# Yield Sync Strategy

- Should return the return amount of each token per ERC-20
- Should return the price of each token utilized

## Notes

PA = Percent Allocation

a(x) = amount of x

P(x) = Price of x

T = set of all tokens

t = t is element of T or t ∈ T

PA = (a(t1) * P(t)) / (∑ t ∈ T a(t) * P(t))

### Idea for Strategy

- Consider implementing an insurance mechanism

