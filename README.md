// SPDX-License-Identifier: MIT
pragma solidity ^0.8.0;

contract SocialMediaEngagement {
    mapping(address => uint256) public engagementScores; // Store engagement score of each address
    mapping(address => uint256) public rewards; // Store rewards for each address

    // Event to log engagement updates
    event EngagementUpdated(address indexed user, uint256 newEngagementScore);
    // Event to log reward claims
    event RewardClaimed(address indexed user, uint256 rewardAmount);

    // Method to record a user's engagement (likes, comments, shares, etc.)
    function updateEngagement(address user, uint256 engagementPoints) public {
        engagementScores[user] += engagementPoints;
        emit EngagementUpdated(user, engagementScores[user]);
    }

    // Method to calculate reward based on engagement
    function calculateReward(address user) public {
        uint256 score = engagementScores[user];
        // Simple reward logic, for example: 1 token for every 10 engagement points
        uint256 reward = score / 10;
        rewards[user] = reward;
    }

    // Method for users to claim their reward
    function claimReward() public {
        uint256 rewardAmount = rewards[msg.sender];
        require(rewardAmount > 0, "No rewards available to claim");

        // Transfer the reward (this is simplified; in a real contract, you would interact with an ERC20 token contract)
        rewards[msg.sender] = 0; // Reset reward after claiming

        // Emit event for reward claim
        emit RewardClaimed(msg.sender, rewardAmount);
        
        // Logic to actually send the reward would be placed here (e.g., transferring ERC20 tokens).
    }

    // Method to get the user's current engagement score
    function getEngagementScore(address user) public view returns (uint256) {
        return engagementScores[user];
    }

    // Method to get the user's current reward
    function getReward(address user) public view returns (uint256) {
        return rewards[user];
    }
}
