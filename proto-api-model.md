# searchAssignFields API Response vs Proto vs Java Model — Comparison

## MISMATCH SUMMARY

## **1. DATA TYPE MISMATCHES — API vs Proto**

| API Field Path | API Type | Proto Type | Java Type | **Issue** |
|---|---|---|---|---|
| `transactionContext.paymentTransaction.transaction.availableFunds` | double | int64 | double | **API matches Java but NOT proto (proto says int64)** |
| `transactionContext.paymentTransaction.transaction.token.assuranceLevel` | **string** | int64 | int | **API says `string`, proto says `int64`, Java says `int` — ALL THREE DISAGREE** |
| `transactionContext.paymentTransaction.device.latitude` | float | double | float | **API matches Java but NOT proto (proto says double)** |
| `transactionContext.paymentTransaction.device.longitude` | float | double | float | **API matches Java but NOT proto (proto says double)** |
| `transactionContext.paymentTransaction.paymentInstrument.panInformation.limits.creditLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.paymentTransaction.paymentInstrument.panInformation.limits.dailyCashLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.paymentTransaction.paymentInstrument.panInformation.limits.overdraftLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.paymentTransaction.transaction.posting.date` | **timestamp** | google.type.Date | LocalDate | **API says `timestamp`, should be `date`** |
| `transactionContext.bankingTransaction.debtor.amount.value` | float | double | double | **API says `float`, proto/Java say `double`** |
| `transactionContext.bankingTransaction.debtor.amount.currencyConversionRate` | float | double | double | **API says `float`, proto/Java say `double`** |
| `transactionContext.bankingTransaction.creditor.amount.value` | float | double | double | **API says `float`, proto/Java say `double`** |
| `transactionContext.bankingTransaction.creditor.amount.currencyConversionRate` | float | double | double | **API says `float`, proto/Java say `double`** |
| `transactionContext.bankingTransaction.debtor.device.latitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.bankingTransaction.debtor.device.longitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.bankingTransaction.creditor.device.latitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.bankingTransaction.creditor.device.longitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.bankingTransaction.transaction.order.recurringFrequency` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.device.latitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.activityEvent.device.longitude` | float | double | float | **API matches Java but NOT proto** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.delinquency.delinquentAmount` | float | double | float | **API matches Java but NOT proto (precision loss)** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.delinquency.currencyConversionRate` | float | double | float | **API matches Java but NOT proto (precision loss)** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.account.limits.creditLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.account.limits.overdraftLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.account.limits.dailyPosLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.account.limits.dailyCashLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.account.limits.dailyTotalLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.monetaryLimits.creditLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.monetaryLimits.dailyCashLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.monetaryLimits.dailyPosLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.monetaryLimits.overdraftLimit` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.pinInformation.pinLength` | int | int64 | int | **API matches Java `int` but NOT proto `int64`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.panInformation.limits.creditLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.panInformation.limits.dailyCashLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.panInformation.limits.overdraftLimit` | double | int64 | int | **API says `double`, proto says `int64`, Java says `int`** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.token.assuranceLevel` | integer | int64 | int | **API matches Java `int` but NOT proto `int64`** |

---

## **2. FIELD NAME MISMATCHES — API vs Proto/Java**

| API Field Path | **Issue** | Expected Name |
|---|---|---|
| `transactionContext.paymentTransaction.paymentInstrument.panInformation.limits.dailyMerchandise` | **MISMATCH: field name truncated** | Should be `dailyMerchandiseLimit` (proto) / `dailyMerchandiseLimit` (Java) |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.panInformation.limits.dailyMerchandise` | **MISMATCH: field name truncated** | Should be `dailyMerchandiseLimit` (proto) / `dailyMerchandiseLimit` (Java) |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.customer.isPrimaryAddress` | **MISMATCH: wrong field name** | Should be `isPrimary` (proto `is_primary`) — `isPrimaryAddress` doesn't exist in Customer |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.cardholder.location.*` | **Path uses `cardholder` instead of `cardHolder`** | Proto/Java class is `CardHolder` -> should be `cardHolder` |
| `transactionContext.bankingTransaction.transaction.processingChannel.subType` | **MISMATCH: API uses `subType`** | Proto field is `subtype` (no camelCase), Java is also `subtype` |

---

## **3. FIELDS IN API RESPONSE THAT DON'T EXIST IN PROTO**

| API Field Path | API Type | **Issue** |
|---|---|---|
| `transactionContext.paymentTransaction.transaction.walletType` | string | **FIELD DOES NOT EXIST in proto `PaymentTransactionInfo` or Java `Transaction`** |
| `transactionContext.activityEvent.transaction.nonmonCode` | string | **EXISTS in Java only (EXTRA IN JAVA), NOT in proto** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.actionCode` | string | **EXISTS in Java `NonmonCodeDetailsNew` only, NOT in proto at this level (moved from `NonmonCodeDetails.action_code`)** |
| `efsFeatures.name` / `efsFeatures.value` | string | **Different naming from 2nd/3rd response (`features.name`/`features.value`)** |

---

## **4. FIELDS IN PROTO/JAVA BUT MISSING FROM API RESPONSE**

### Payment Transaction — Missing Fields

| Proto/Java Field Path | Type | **Status** |
|---|---|---|
| `transactionContext.paymentTransaction.header.customerAccountNumber` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.beneficiaryAccountNumber` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.customerId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.beneficiaryCustomerId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.deviceId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.ipAddress` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.userId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.pan.pan` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.pan.expandedBin` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.terminalId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.merchantId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.bankId` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.header.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.paymentTransaction.merchant.ownershipType` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.device.screenResolution` | string | **MISSING from API** |
| `transactionContext.paymentTransaction.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.paymentTransaction.merchant.terminal.posUnattended` | string | **MISSING from API** — wait, it's present |

### Banking Transaction — Missing Fields

| Proto/Java Field Path | Type | **Status** |
|---|---|---|
| `transactionContext.bankingTransaction.header.customerAccountNumber` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.beneficiaryAccountNumber` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.customerId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.beneficiaryCustomerId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.deviceId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.ipAddress` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.userId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.pan.pan` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.pan.expandedBin` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.terminalId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.merchantId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.bankId` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.header.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.bankingTransaction.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.bankingTransaction.creditor.device.screenResolution` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.creditor.merchant.atmOwner` | string | **MISSING from API** |
| `transactionContext.bankingTransaction.session.language` | string | **Present in API (GOOD)** |

### Activity Event — Missing Fields

| Proto/Java Field Path | Type | **Status** |
|---|---|---|
| `transactionContext.activityEvent.header.customerAccountNumber` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.beneficiaryAccountNumber` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.customerId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.beneficiaryCustomerId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.deviceId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.ipAddress` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.userId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.pan.pan` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.pan.expandedBin` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.terminalId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.merchantId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.bankId` | string | **MISSING from API** |
| `transactionContext.activityEvent.header.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.activityEvent.extensions` | List\<CustomField\> | **MISSING from API** |
| `transactionContext.activityEvent.session.language` | string | **MISSING from API** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.customerType.type` | string | **MISSING from API (only `vipType` is present)** |
| `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.passport.expirationDate` | date | **MISSING from API** |

---

## **5. INCONSISTENCIES BETWEEN THE 3 API RESPONSES**

| Field Concept | Response 1 (Card) Path | Response 2/3 (Banking/NMON) Path | **Issue** |
|---|---|---|---|
| Features | `efsFeatures.name` / `efsFeatures.value` | `features.name` / `features.value` | **INCONSISTENT: different root path names** |
| Model Scores | `modelScores.scores.*` | `scores.modelScores.*` | **INCONSISTENT: path structure is reversed** |
| Rules | Not present | `rules.ruleName`, `rules.ruleDecisions.*` | **Missing from Card response** |
| Hotlists | `hotlists.name` / `hotlists.value` | `hotlists.name` / `hotlists.value` | Consistent |

---

## **6. LOCATION FIELD PATH MISMATCHES — Proto `Location` vs API Usage**

The proto defines a `Location` message with fields: `city`, `stateProvince`, `postalCode`, `countryCode`

But in the Banking Transaction debtor/creditor, the API uses `cardholderCity`, `cardholderStateProvince`, etc. which comes from the `CardLocation`/`pitran.Location` class (designed for PAN information), NOT the generic `Location` class.

| API Field Path | API Field Name | **Expected (from Proto `Location`)** | **Issue** |
|---|---|---|---|
| `transactionContext.bankingTransaction.debtor.location.cardholderCity` | cardholderCity | `city` | **MISMATCH: Using CardLocation fields instead of Location fields** |
| `transactionContext.bankingTransaction.debtor.location.cardholderStateProvince` | cardholderStateProvince | `stateProvince` | **MISMATCH** |
| `transactionContext.bankingTransaction.debtor.location.cardholderCountryCode` | cardholderCountryCode | `countryCode` | **MISMATCH** |
| `transactionContext.bankingTransaction.debtor.location.cardholderPostalCode` | cardholderPostalCode | `postalCode` | **MISMATCH** |
| `transactionContext.bankingTransaction.creditor.location.cardholderCity` | cardholderCity | `city` | **MISMATCH** |
| `transactionContext.bankingTransaction.creditor.location.cardholderStateProvince` | cardholderStateProvince | `stateProvince` | **MISMATCH** |
| `transactionContext.bankingTransaction.creditor.location.cardholderCountryCode` | cardholderCountryCode | `countryCode` | **MISMATCH** |
| `transactionContext.bankingTransaction.creditor.location.cardholderPostalCode` | cardholderPostalCode | `postalCode` | **MISMATCH** |

**Root Cause:** The Java model for `Debtor` and `Creditor` imports `pitran.Location` (which has `cardholder*` prefixed fields) instead of `common.Location` or the proto's generic `Location` message (which has plain `city`, `stateProvince`, etc.). This was also flagged in the proto-vs-Java comparison.

---

## **7. `nonmonCodeDetails.new` PATH ISSUE**

In the API response, the path uses `.new.` which corresponds to the proto field named `new` (a Java reserved word). In Java this is `nonmonCodeDetailsNew` with `@JsonProperty("new")`.

The API correctly serializes as `.new.` in the JSON path (matching the proto field name and `@JsonProperty` annotation). However, the intermediate object name `nonmonCodeDetails` maps to `NonmonCodeDetails` message, and inside it the `new` field references `NonmonCodeDetailsNew`.

**Observation:** The API path `transactionContext.activityEvent.transaction.nonmonCodeDetails.new.*` is **correct** — it follows the JSON serialization path, not the Java field name.

---

## **8. CRITICAL MISMATCH: `walletType` FIELD**

| API Field Path | API Type | Proto | Java | **Issue** |
|---|---|---|---|---|
| `transactionContext.paymentTransaction.transaction.walletType` | string | **DOES NOT EXIST** | **DOES NOT EXIST** | **Field exists ONLY in API response — phantom field with no backing in proto or Java model** |

This is the most critical mismatch — the API exposes a field that has no definition in either the proto contract or the Java data model.

---

## **OVERALL STATISTICS**

| Category | Count |
|---|---|
| **Data type mismatches (API vs Proto)** | **35** |
| **Field name mismatches** | **5** |
| **Phantom fields (in API but not in proto/Java)** | **1** (`walletType`) |
| **Fields using Java-only additions** | **2** (`nonmonCode`, `actionCode`) |
| **Missing header fields across all 3 responses** | **~36** (12 per response) |
| **Location field path mismatches** | **8** |
| **Cross-response inconsistencies** | **3** (features path, scores path, rules presence) |
| **Total discrepancies** | **~90** |

