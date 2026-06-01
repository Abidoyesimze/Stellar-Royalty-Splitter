## #328 BUG: No request size limit on distribute endpoint

### Description
No request size limit on the distribute endpoint. The backend accepts unbounded request payloads. A large malicious payload could cause memory pressure.

### Scope of Work
- Add Express express.json({ limit: '10kb' }) middleware
- Apply size limit to all routes
- Return 413 Payload Too Large on oversized requests
- Add tests for size limit enforcement
### Reference
- Current middleware in backend
- Express documentation
### Out of Scope
- Modifying the request parsing logic
- Adding other size limits
### Acceptance Criteria
- Request size limit is enforced
- Oversized requests return 413
- Limit is applied to all routes
- Tests pass on Linux CI
- No breaking changes to existing API
### Note for Contributors
- Use existing middleware patterns
- Consider legitimate request sizes
- Update API.md documentation
## #329 ENHANCEMENT: Add /contract/info endpoint

### Description
Add a /contract/info endpoint. Return current on-chain contract state: admin address, royalty rate, recipient list, contract balance, and network. Useful for frontend initialization and operator dashboards without requiring a separate Horizon query.

### Scope of Work
- Add /contract/info endpoint
- Return admin address
- Return royalty rate
- Return recipient list
- Return contract balance
- Return current network
### Reference
- Current backend routes
- Contract state in Soroban
### Out of Scope
- Adding other contract information
- Modifying the contract
### Acceptance Criteria
- /contract/info endpoint exists
- Returns all required information
- Information is current
- Tests pass on Linux CI
- No breaking changes to existing API
### Note for Contributors
- Use existing endpoint patterns
- Consider caching for performance
- Update API.md documentation

## #330 ENHANCEMENT: Add Prometheus metrics endpoint
### Description
Add Prometheus metrics endpoint. Expose /metrics with counters for total distribute calls, successful transactions, failed transactions, and average Horizon response time. Makes the backend observable in production without log scraping.

### Scope of Work
- Add Prometheus metrics endpoint
- Track total distribute calls
- Track successful transactions
- Track failed transactions
- Track average Horizon response time
### Reference
- Prometheus documentation
- Current backend metrics
### Out of Scope
- Adding other metrics
- Modifying the transaction logic
### Acceptance Criteria
- /metrics endpoint exists
- Metrics are tracked correctly
- Prometheus format is used
- Tests pass on Linux CI
- No breaking changes to existing API
### Note for Contributors
- Use existing metrics patterns
- Consider performance impact
- Update API.md documentation

## #332 ENHANCEMENT: Add scripts/seed.ts for local development
### Description
Add a scripts/seed.ts for local development. A script that deploys the contract to Testnet, initializes it with a test admin, sets a royalty rate, and funds the contract account so contributors can get a working local environment in one command.

### Scope of Work
- Create scripts/seed.ts script
- Deploy contract to Testnet
- Initialize with test admin
- Set royalty rate
- Fund contract account
### Reference
- Current deployment process
- Stellar CLI documentation
### Out of Scope
- Adding other setup steps
- Automating deployments
### Acceptance Criteria
- scripts/seed.ts exists
- Contract is deployed
- Contract is initialized
- Royalty rate is set
- Contract is funded
### Note for Contributors
- Test script locally
- Document all required environment variables
- Add error handling

