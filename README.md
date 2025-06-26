# CodeAlpha_Multi-Send-Smart-Contract
CodeAlpha Internship Task 2
Source Code- // SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;
contract MultiSend {
    function multiSend(address[] calldata recipients) external payable {
        uint256 totalRecipients = recipients.length;
        require(totalRecipients > 0, "No recipients provided");
        uint256 amountPerRecipient = msg.value / totalRecipients;
        require(amountPerRecipient > 0, "Insufficient Ether to split");
        for (uint256 i = 0; i < totalRecipients; i++) {
            (bool success, ) = recipients[i].call{value: amountPerRecipient}("");
            require(success, "Transfer failed");
        }
    }
}
