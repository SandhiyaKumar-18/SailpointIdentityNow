# SailPoint IdentityNow: Configuring Authoritative and Non-Authoritative Sources

## Sources in SailPoint IdentityNow

In IdentityNow, a **source** represents a system or application that contains identity or access data. There are two types:

1. **Authoritative Source**
   - Provides **primary identity data** (employee records, personal attributes).
   - Typically an HR system (e.g., Workday, SAP SuccessFactors) or AD in some cases.
   - IdentityNow uses this to **create and update identities** in the Identity Cube.

2. **Non-Authoritative Source**
   - Provides **access data** (entitlements, accounts) but does **not control identity creation**.
   - Examples: SaaS apps, AD groups, SharePoint, Salesforce.
   - IdentityNow **aggregates accounts and entitlements** from these sources to know what access exists.

## Steps to Configure Sources

### 1. Authoritative Source
1. Go to **Admin → Setup → Sources** in IdentityNow.
2. Click **“Add Source”**.
3. Select the source type (e.g., Workday, AD).
4. Configure connection details:
   - Host / API URL  
   - Credentials (service account)  
   - Connection type (SOAP/REST/LDAP/SCIM)
5. Define **Identity Profile mapping**:
   - Map source attributes → Identity Cube attributes (e.g., `employeeId`, `email`, `department`)  
   - Choose **unique identifier** for identity correlation.
6. Set as **Authoritative**.
7. Test the connection, and **aggregate identities**.
8. Save and schedule **identity refresh/aggregation**.

### 2. Non-Authoritative Source
1. Go to **Admin → Setup → Sources**.
2. Click **“Add Source”**.
3. Select the application type (SaaS, LDAP, AD, database, etc.).
4. Configure connection details:
   - Host, credentials, connection type.
5. Map entitlements / account attributes to Identity Cube:
   - Example: AD groups → Entitlements  
   - Email → Account username
6. Set as **Non-Authoritative**.
7. Test the connection and **aggregate accounts & entitlements**.
8. Save and schedule regular **entitlement refresh**.

## Best Practices
- **Authoritative Source = Single Source of Truth**
  - Typically HR system → keeps identity attributes consistent.
- **Non-Authoritative Sources = Access aggregation only**
  - Never create identities from non-authoritative sources; just read their entitlements.
- **Test everything** before scheduling aggregation to avoid data corruption.
- **Use Virtual Appliances** for on-premise sources (like AD) to securely connect to the cloud.

## Interview Answer (Concise)
*"In IdentityNow, authoritative sources (like HR systems) provide primary identity data and are used to create and update the Identity Cube. Non-authoritative sources (like AD, SaaS apps) provide entitlements and account data. Configuration involves adding the source in Admin → Setup → Sources, mapping attributes, testing the connection, and scheduling aggregation."*
