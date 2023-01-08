# Utilizing LZN In Apocalypse

## <mark style="color:yellow;">LZN Utility In Apocalypse</mark>

The Luzion Protocol (LZN) token will be utilized in our Apocalypse ecosystem game to ensure its perpetual sustainability through player buying and selling. During PVP and Battle Royale gameplay, players can use LZN by staking it as collateral. Each staking transaction will incur a transfer tax, but there will be no tax on winning withdrawals.

Players who create a PVP room can stake any desired amount of LZN, while players joining a PVP battle must match the stake of the room creator. In Battle Royale, the system sets a required amount of LZN that must be staked.

Utilization of LZN in Apocalypse PVP and Battle Royale generates a significant volume of transactions, complete with taxation, which ensures constant automated token burning and auto liquidity injection. The ecosystem and marketing wallets will also be replenished for future development and use cases.

As LZN is constantly rebasing, every LZN that enters the PVP or Battle Royale smart contracts will slightly increase in value after each epoch. To counteract this, any additional tokens will be transferred to the burn address, effectively stabilizing the inflation rate and increasing the black hole supply over time.

### <mark style="color:yellow;">How Does It Work?</mark>

The player versus player (PVP) function is designed to facilitate combat between two players using their respective non-fungible tokens (NFTs) as avatars. The creator of the PVP room, which is located within the PVP smart contract, initiates a PVP transaction by inviting a second player to join the room. Once the second player accepts the invitation, the PVP is automatically triggered and both players receive their results, including any stake rewards, upon completion of the battle.

In addition to stake rewards, players also have the opportunity to receive an airdrop of NFT minerals upon losing a PVP battle. These airdrops, which are distributed on a chance basis, serve to compensate players for their losses and provide an additional incentive for participating in PVP. As a result, players are not solely reliant on stake rewards as a means of gain, but also have the potential to acquire valuable NFT minerals through the airdrop system.

1. A player creates a PVP room within the PVP smart contract by selecting their NFT character.
2. Another player is invited to join the PVP room and chooses their NFT character to participate in combat.
3. The PVP transaction is automatically triggered upon the second player accepting the invitation to join the room.
4. The PVP battle takes place, and both players receive their results, including any stake rewards, upon completion.
5. If a player loses the PVP battle, they have a chance to receive an airdrop of NFT minerals as compensation.
6. The process can be repeated as desired, with players able to create or join additional PVP rooms and engage in further combat.
7. Players have the ability to review their past win/loss data at any time at history tab.

### <mark style="color:yellow;">PVP Logic Code Section</mark>

{% code overflow="wrap" lineNumbers="true" %}
```solidity
/* PvP logic */

    /**
     * @dev Create a new PvP listing.
     */
    function createPvPRoom(uint256 _charID, uint256 _price) external payable whenNotPaused nonReentrant {

        uint256 _amount = checkPrice(minStake, rewardToken);

        if (allowMultipleRoom == false) {
            require(getCurrentPvPIDForCharacter[_charID] == 0 , "There's an active PvP room for this character!");
        }
        require(_price >= _amount, "Price must be greater than the minimum amount allowed!");
        require(apocCharacter.ownerOf(_charID) == _msgSender(), "You are not the owner of this character!");

        _pvpID.increment();
        uint256 _getPvPID = _pvpID.current();

        idToPvPInfo[_getPvPID] =  pvpInfo(_getPvPID, _price, _charID, 0, false, payable(_msgSender()), payable(ZERO));
        getCurrentPvPIDForCharacter[_charID] = _getPvPID;
        
        rewardToken.transferFrom(_msgSender(), address(this), _price);
        totalStake = totalStake.add(_price);

        emit CreatePvPRoom(_getPvPID, _msgSender(), _amount);
    }

    /**
     * @dev Join listed PvP room.
     */
    function joinPvPRoom(uint256 _charID, uint256 _roomID) external payable whenNotPaused nonReentrant {

        require(_roomID > 0 && _roomID <= _pvpID.current(), "This PvP fight does not exist!");
        require(idToPvPInfo[_roomID].fight == false, "This PvP fight already ended!");
        require(apocCharacter.ownerOf(_charID) == _msgSender(), "You are not the owner of this character!");
        require(idToPvPInfo[_roomID].player1 != _msgSender(), "You cannot join the PvP room that you created!");

        uint256 _amount = idToPvPInfo[_roomID].amountToStake;
        
        rewardToken.transferFrom(_msgSender(), address(this), _amount);
        totalStake = totalStake.sub(_amount);

        idToPvPInfo[_roomID].player2 = payable(_msgSender());
        idToPvPInfo[_roomID].charIDP2 = _charID;
        
        emit JoinPvPRoom(_roomID, _msgSender(), _amount);
        
        uint256 _tax = _amount.mul(rewardTax[0]).div(rewardTax[1]);
        uint256 _winnerReward = (_amount.sub(_tax)).mul(2);

        address _player1 = idToPvPInfo[_roomID].player1;
        address _player2 = idToPvPInfo[_roomID].player2;
        uint256 _status; 
        uint256 _drop; 
        (_status , _drop) = mixer(_player1, _player2);

        if (_status == 0) {
            IERC20Extended(rewardToken).transfer(_player1, _winnerReward);
            fightWon[_player1] = fightWon[_player1] + 1;
            dropMineral(_player2);
            fightLost[_player2] = fightLost[_player2] + 1;
            emit PvPCompleted(_roomID, _player1, _player2);
        } else if (_status == 1) {
            IERC20Extended(rewardToken).transfer(_player2, _winnerReward);
            fightWon[_player2] = fightWon[_player2] + 1;
            dropMineral(_player1);
            fightLost[_player1] = fightLost[_player1] + 1;
            emit PvPCompleted(_roomID, _player2, _player1);
        }
                
        idToPvPInfo[_roomID].fight = true;
        _pvpFought.increment();

        getCurrentPvPIDForCharacter[idToPvPInfo[_roomID].charIDP1] = 0;

        if (allowPot == true) {
            (address potWinnerAddress, bool distributeStatus) = apocPot.distributePot(_player1, _player2);

            if (distributeStatus == true) {
                emit PotDistributed(potWinnerAddress);
            }
        }

        uint256 pot = rewardToken.balanceOf(address(this)).sub(totalStake).mul(potDistribution[0]).div(potDistribution[1]);
        require(rewardToken.transferFrom(address(this), address(apocPot), pot));

    }

    /**
     * @dev Cancel PvP room session.
     */
    function cancelPvPRoom(uint256 _roomID) external payable nonReentrant {
            
        uint256 _staked = idToPvPInfo[_roomID].amountToStake;
        address _creator = idToPvPInfo[_roomID].player1;
        address _competitor = idToPvPInfo[_roomID].player2;
        bool _fight = idToPvPInfo[_roomID].fight;

        require(_msgSender() == _creator, "You are not the creator for this PvP room session.");
        require(_fight == false && _competitor == payable(ZERO), "This NFT has either been sold or the listing was already canceled");
        
        idToPvPInfo[_roomID].player2 = payable(_msgSender());
        _pvpCanceled.increment();

        idToPvPInfo[_roomID].fight = true;
        
        if (cancelTax[0] > 0) {
            uint256 _tax = _staked.mul(cancelTax[0]).div(cancelTax[1]);
            require(rewardToken.transferFrom(address(this), _msgSender(), _staked.sub(_tax)));
        } else {
            require(rewardToken.transferFrom(address(this), _msgSender(), _staked));
        }
        totalStake = totalStake.sub(_staked);

        emit PvPCancelled(_roomID, _msgSender());
    }
    
    /**
     * @dev Fetch all active PvP sessions.
     */
    function fetchActivePvP() external view returns (pvpInfo[] memory) {
        
        uint256 _pvpCount = _pvpID.current();
        uint256 _activePvPCount = _pvpID.current() - _pvpFought.current() - _pvpCanceled.current();
        uint256 _currentIndex = 0;

        pvpInfo[] memory items = new pvpInfo[](_activePvPCount);
        
        for (uint256 i = 0; i < _pvpCount; i++) {
            if (idToPvPInfo[i + 1].player2 == ZERO) {
                uint256 currentID = i + 1;
                pvpInfo storage currentItem = idToPvPInfo[currentID];
                items[_currentIndex] = currentItem;
                _currentIndex += 1;
            }
        }

        return items;
    }

    /**
     * @dev Fetch all completed PvP sessions.
     */
    function fetchCompletedPvP() external view returns (pvpInfo[] memory) {
        
        uint256 _currentIndex = 0;

        pvpInfo[] memory items = new pvpInfo[](_pvpFought.current());
        
        for (uint256 i = 0; i < _pvpID.current(); i++) {
            if (idToPvPInfo[i + 1].fight == true && idToPvPInfo[i + 1].player1 != idToPvPInfo[i + 1].player2) {
                uint256 currentID = i + 1;
                pvpInfo storage currentItem = idToPvPInfo[currentID];
                items[_currentIndex] = currentItem;
                _currentIndex += 1;
            }
        }

        return items;
    }

    /**
     * @dev Fetch all cancelled PvP sessions.
     */
    function fetchCancelledPvP() external view returns (pvpInfo[] memory) {
        
        uint256 _currentIndex = 0;

        pvpInfo[] memory items = new pvpInfo[](_pvpCanceled.current());
        
        for (uint256 i = 0; i < _pvpID.current(); i++) {
            if (idToPvPInfo[i + 1].fight == true && idToPvPInfo[i + 1].player1 == idToPvPInfo[i + 1].player2) {
                uint256 currentID = i + 1;
                pvpInfo storage currentItem = idToPvPInfo[currentID];
                items[_currentIndex] = currentItem;
                _currentIndex += 1;
            }
        }

        return items;
    }
}
```
{% endcode %}
