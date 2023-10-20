# Asset Allocator Deployer

## Requirement

1. Must deploy Asset Allocator
2. Must have a feature to collect deployments fee
	- Fee >= 0

3. Must be able to calculate the percent-allocation of a strategy

PA = percent-allocation

a(x) = amount of x

P(x) = price of x

T = set of all tokens

t = element of T or t ∈ T

PA = (a(t1) * P(t)) / (∑ t ∈ T a(t) * P(t))