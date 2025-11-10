
```rust
let infrastructure_trends = InfrastructureTrends {
	region: row.region,
	main_island: row.main_island,
	total_budget: 0.0,
	median_savings: 0.0,
	avg_delay: 0.0,
	high_delay_pct: 0.0,
	efficiency_score: 0.0
};
```


# Total Budget
- aggregate total ApprovedBudgetForContract

# Median Savings
- CostSavings = ApprovedBudgetForContract - ContractCost

# AVG Delay
- CompletionDelayDays = days between StartDate and ActualCompletionDate (positive if delayed)

# High Delay PCT
- percentage of projects with delays > 30 days by Region and MainIsland

# Efficieny Score
- efficiency_score = (median_savings / avg_delay) * 100
