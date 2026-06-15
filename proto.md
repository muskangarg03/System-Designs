# MISMATCH SUMMARY — ALL HIGHLIGHTED ISSUES

---

## **1. DATA TYPE MISMATCHES (26 fields)**

| Proto Message | Field | Proto Type | Java Type | **Issue** |
|---|---|---|---|---|
| **AccountLimits** | credit_limit | int64 | int | **Should be `long`** |
| **AccountLimits** | overdraft_limit | int64 | int | **Should be `long`** |
| **AccountLimits** | daily_pos_limit | int64 | int | **Should be `long`** |
| **AccountLimits** | daily_cash_limit | int64 | int | **Should be `long`** |
| **AccountLimits** | daily_total_limit | int64 | int | **Should be `long`** |
| **CardToken** | assurance_level | int64 | int | **Should be `long`** |
| **Delinquency** | delinquent_amount | double | float | **Precision loss** |
| **Delinquency** | currency_conversion_rate | double | float | **Precision loss** |
| **Device** | latitude | double | float | **Precision loss** |
| **Device** | longitude | double | float | **Precision loss** |
| **Limits** | credit_limit | int64 | int | **Should be `long`** |
| **Limits** | overdraft_limit | int64 | int | **Should be `long`** |
| **Limits** | daily_merchandise_limit | int64 | int | **Should be `long`** |
| **Limits** | daily_cash_limit | int64 | int | **Should be `long`** |
| **MonetaryLimits** | credit_limit | int64 | int | **Should be `long`** |
| **MonetaryLimits** | overdraft_limit | int64 | int | **Should be `long`** |
| **MonetaryLimits** | daily_pos_limit | int64 | int | **Should be `long`** |
| **MonetaryLimits** | daily_cash_limit | int64 | int | **Should be `long`** |
| **Order** | recurring_frequency | int64 | int | **Should be `long`** |
| **PaymentTransactionInfo** | available_funds | int64 | double | **Incompatible types** |
| **PinInformation** | pin_length | int64 | int | **Should be `long`** |
| **Token** | number_of_active_tokens | int64 | int | **Should be `long`** |
| **Token** | wallet_account_age | int64 | int | **Should be `long`** |
| **Token** | assurance_level | int64 | int | **Should be `long`** |
| **TransactionalCaseContext** | transaction_id | string | UUID | **Different representation** |
| **TransactionalCaseContext** | efs_header | Header | EfsHeader | **Different class** |

---

## **2. FIELDS PRESENT IN PROTO BUT MISSING IN JAVA (6 fields)**

| Proto Message | **Missing Field** | Proto Type |
|---|---|---|
| **AccountStatus** | **account_type** | string |
| **CustomerCaseContext** | **customer_type** | string |
| **NonmonCodeDetails** | **action_code** | string |
| **OrgInfo** | **ou_id** | string **(entire class missing)** |
| **OrgInfo** | **su_id** | string **(entire class missing)** |
| **SecondFactorAuthentication** | **active_indicator** | string **(missing in rbtran version)** |

---

## **3. FIELDS PRESENT IN JAVA BUT MISSING IN PROTO (16 fields)**

| Java Class | **Extra Field** | Java Type |
|---|---|---|
| **ApplicationContext** | **organizationUnit** | String |
| **ApplicationContext** | **segmentationUnit** | String |
| **ApplicationContext** | **customerId** | String |
| **ApplicationContext** | **customerAccountNumber** | String |
| **ApplicationContext** | **pan** | String |
| **ApplicationContext** | **createTime** | Instant |
| **ApplicationContext** | **createUser** | String |
| **ApplicationContext** | **updateTime** | Instant |
| **ApplicationContext** | **updateUser** | String |
| **Transaction (nmon)** | **nonmonCode** | String |
| **Transaction (pitran)** | **authenticationMethod** | String |
| **PaymentInstrument (pitran)** | **pan** | Pan |
| **PaymentInformation (pis)** | **id** | UUID |
| **PaymentInformation (pis)** | **name** | String |
| **PaymentInformation (pis)** | **expandedBin** | String |
| **NonmonCodeDetailsNew** | **actionCode** | String **(moved from NonmonCodeDetails)** |

---

## **4. CLASS NAME MISMATCHES (13 mappings)**

| Proto Message Name | **Java Class Name** | Java Location |
|---|---|---|
| **AccountDetails** | **Account** | customerdetails/ais/ |
| **AccountLimits** | **Limits** | customerdetails/ais/ |
| **AccountTypeInfo** | **AccountType** | customerdetails/ais/ |
| **ActivityEventTransaction** | **Transaction** | transactions/nmon/ |
| **ApplicationCaseContext** | **ApplicationContext** | casecontext/ |
| **BankingTransactionInfo** | **Transaction** | transactions/rbtran/ |
| **CardHolderLocation** | **Location** | customerdetails/pis/ |
| **CardLocation** | **Location** | transactions/pitran/ |
| **CardPaymentInstrument** | **PaymentInstrument** | customerdetails/pis/ |
| **CardToken** | **Token** | customerdetails/pis/ |
| **CustomerCaseContext** | **CustomerContext** | casecontext/ |
| **PaymentTransactionInfo** | **Transaction** | transactions/pitran/ |
| **TransactionalCaseContext** | **TransactionContext** | casecontext/ |

---

## **5. FIELD NAME MISMATCHES (2 fields — reserved word conflicts)**

| Proto Message | Proto Field | **Java Field** | **Reason** |
|---|---|---|---|
| **Aip** | `static` | **`staticValue`** | **Reserved word in Java, uses `@JsonProperty("static")`** |
| **NonmonCodeDetails** | `new` | **`nonmonCodeDetailsNew`** | **Reserved word in Java, uses `@JsonProperty("new")`** |

---

## **6. SPLIT CLASS ISSUES**

| Proto Message | **Issue** |
|---|---|
| **SecondFactorAuthentication** | **Split across 2 Java classes: `rbtran` version has (`method`, `result`) but MISSING `activeIndicator`; `cis` version has (`method`, `activeIndicator`) but MISSING `result`. Neither version has all 3 proto fields.** |
| **PanInformation** | **Full version in `pitran` (15 fields); reduced version in `pis` (only 7 fields) used by PaymentInformation** |
