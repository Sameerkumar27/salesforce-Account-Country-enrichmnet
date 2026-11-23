# Account Country Enrichment

## About Project
This project automatically fetches country details for Salesforce Accounts using the REST Countries API.

Whenever an Account is created or its Billing Country is changed, the system fetches the country information and updates the Account.

## Technologies Used
- Salesforce Apex
- Apex Triggers
- Queueable Apex
- Future Methods
- REST API
- JSON

## Country Details
- Capital
- Region
- Currency
- Enrichment Status (Success / Failed)

## How It Works
1. Account Trigger detects new or updated Accounts.
2. Handler checks whether Billing Country needs enrichment.
3. Queueable Apex processes the records asynchronously.
4. CountryApiService calls the REST Countries API.
5. Account fields are updated with the response.

## Future vs Queueable

**Q1. Why does Future accept Set<Id> but not List<Account>?**

Future methods do not support sObjects as parameters. That's why we pass Account IDs and query the records inside the method.

**Q2. What can Queueable do that Future cannot?**

- Queueable can accept complex objects like sObjects.
- Queueable returns a job ID to monitor its execution.
- Queueable also supports job chaining.
- Future method can not call Future method.

## Testing
Tested the following cases:
- Successful API response
- Country not found (404)
- Server error (500)
- Bulk processing of 50 Accounts
- Update without changing Billing Country

## Note
API authentication is required. The API key should be configured securely and should not be uploaded to GitHub.
