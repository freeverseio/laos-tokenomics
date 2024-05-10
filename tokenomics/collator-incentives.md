# 🌐 Collator Incentives

<mark style="color:green;">**Collators are the cornerstone of the LAOS Parachain**</mark>, ensuring data availability, lack of censorship, and overall system robustness. While collators also validate transactions, the final validation of each block is ultimately confirmed by the Polkadot Relay Chain. Mid-term, the LAOS parachain will transition to a sharding-based approach, enabling horizontal scaling. In this phase, part of the security will be reliant on the validators of the LAOS Relay Chain. Incentivization is crucial to attract and retain a competent set of collators.

To produce blocks, collators are incentivized via _collator incentives_ as well as _transaction fees_.  As detailed [here](inflation-and-fee-model.md), during the first two years, the main source of collator incentives will be paid out programmatically, upon block production, by a especifically allocated <mark style="color:green;">**sub-pool of the Community Incentives Pool,**</mark> originally set out to an approximate 7.5% of the total genesis supply annually. These incentives are allocated for the initial lease period of the parachain slot and inflationary tokens will be used for collator incentives once inflation begins after the first two years.&#x20;

Collators retain a percentage of these rewards, which is initially set to 20%, and the rest is shared among those that delegated on them, proportionally to the amount delegated.

Additionally, _transaction fees_ will be allocated to the block producing collators, as a means to incentivize inclusion of transactions and disincentivize censorship.



