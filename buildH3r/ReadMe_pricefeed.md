Price feed transactions:
setup hash-0x54203d9e7c5128b95b8960b7c9c03d435b222dddb3ea3b1317fa0b299aced6e0

transacition hash-0x1800d23135f6136c0499338d7b1ab39fa7d42b4068705e749f172531ef9fc1dc


Code:
```
// SPDX-License-Identifier: MIT
pragma solidity 0.8.25;

import "@api3/contracts/api3-server-v1/proxies/interfaces/IProxy.sol";
import "@openzeppelin/contracts/access/Ownable.sol";


contract Pricer is Ownable{
    address public  ethPriceFeed;
    address public  dogePriceFeed;
    constructor() Ownable(msg.sender) {}

    function setUp(address _ethPriceFeed, address _dogePriceFeed) external onlyOwner{
        ethPriceFeed = _ethPriceFeed;
        dogePriceFeed = _dogePriceFeed;
    }

    function readEthFeed() public view  returns(uint256, uint256){
        (int224 value, uint256 timestamp) = IProxy(ethPriceFeed).read();
        uint256 price = uint224(value);
        return (price, timestamp);
    }

    function readBitcoinFeed() public view  returns(uint256, uint256){
        (int224 value, uint256 timestamp) = IProxy(dogePriceFeed).read();
        uint256 price = uint224(value);
        return (price, timestamp);
    }
}```