# wallet-risk-scoring-guide2
1. Data Collection Method
Since live blockchain data access isn't possible here, we simulated transaction behavior using realistic distributions (uniform and Poisson) based on typical Compound V2/V3 wallet activities:

Borrow ratios

Liquidation history

Repayment consistency

Stablecoin usage

Token volatility

2. Feature Selection Rationale
Feature	Risk Logic
Borrow Ratio	High borrow ratio = high liquidation risk
Liquidation Count	History of liquidation = poor health
Token Volatility	Riskier if collateral is volatile
Timely Repayment	Good repayment = lower risk
Stablecoin Usage	More stable assets = less risky

3. Risk Scoring Method
We created a composite score out of 1000 using weighted features:

plaintext
Copy
Edit
score = 1000 
       - 400 * borrow_ratio_norm
       - 200 * liquidation_count_norm
       - 100 * token_volatility_norm
       + 200 * timely_repayment_ratio_norm
       + 100 * stablecoin_usage_norm
Features were normalized using min-max scaling

Scores were rounded and clipped between 0 and 1000

Higher score = lower risk

4. Justification & Scalability
Approach aligns with risk frameworks used by DeFi protocols (like Gauntlet, OpenZeppelin audits).

Easily scalable to real data from:

Compound's Subgraph API

Etherscan API

Alchemy or Moralis


