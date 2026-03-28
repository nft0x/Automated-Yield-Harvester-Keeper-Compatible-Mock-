# Automated-Yield-Harvester-Keeper-Compatible-Mock-
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/access/Ownable.sol";

contract YieldHarvester is Ownable {
    uint256 public lastHarvest;
    uint256 public harvestInterval = 1 days;

    event HarvestExecuted(uint256 timestamp, uint256 reward);

    constructor(address initialOwner) Ownable(initialOwner) {
        lastHarvest = block.timestamp;
    }

    function canHarvest() public view returns (bool) {
        return block.timestamp >= lastHarvest + harvestInterval;
    }

    function harvest() external {
        require(canHarvest(), "Too soon");
        lastHarvest = block.timestamp;
        // Add logic to claim rewards from staking/farming contracts
        emit HarvestExecuted(block.timestamp, 100 ether); // demo
    }
}
