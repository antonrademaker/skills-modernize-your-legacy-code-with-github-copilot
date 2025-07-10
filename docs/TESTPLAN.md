# COBOL Account Management System - Test Plan

## Overview

This test plan covers all business logic and functionality of the COBOL Account Management System for student accounts. The test cases are designed to validate the system's behavior and can be used as a basis for creating automated unit and integration tests in Node.js during the modernization process.

## Test Environment

- **System**: COBOL Account Management System
- **Initial Balance**: $1,000.00 (default for all student accounts)
- **Test Data**: Various transaction amounts and scenarios
- **Expected Behavior**: Based on current COBOL implementation

## Test Cases

### Menu and Navigation Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC001 | Display main menu on application start | Application compiled and ready to run | 1. Start application<br>2. Observe initial display | Menu displays with options 1-4:<br>- View Balance<br>- Credit Account<br>- Debit Account<br>- Exit | TBD | TBD | Critical path - system entry point |
| TC002 | Handle valid menu selection (1) | Application running, menu displayed | 1. Enter "1" when prompted<br>2. Observe response | System accepts input and proceeds to View Balance operation | TBD | TBD | Valid input handling |
| TC003 | Handle valid menu selection (2) | Application running, menu displayed | 1. Enter "2" when prompted<br>2. Observe response | System accepts input and proceeds to Credit Account operation | TBD | TBD | Valid input handling |
| TC004 | Handle valid menu selection (3) | Application running, menu displayed | 1. Enter "3" when prompted<br>2. Observe response | System accepts input and proceeds to Debit Account operation | TBD | TBD | Valid input handling |
| TC005 | Handle valid menu selection (4) | Application running, menu displayed | 1. Enter "4" when prompted<br>2. Observe response | System displays "Exiting the program. Goodbye!" and terminates | TBD | TBD | System exit functionality |
| TC006 | Handle invalid menu selection | Application running, menu displayed | 1. Enter "5" when prompted<br>2. Observe response | System displays "Invalid choice, please select 1-4." and redisplays menu | TBD | TBD | Error handling for invalid input |
| TC007 | Handle non-numeric menu input | Application running, menu displayed | 1. Enter "a" when prompted<br>2. Observe response | System handles gracefully and redisplays menu | TBD | TBD | Input validation |
| TC008 | Menu redisplay after operation | Any operation completed | 1. Complete any operation<br>2. Observe display | Menu redisplays after operation completion | TBD | TBD | User experience flow |

### Balance Inquiry Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC009 | View initial balance | Fresh application start | 1. Select option 1<br>2. Observe balance display | Display shows "Current balance: 001000.00" | TBD | TBD | Initial state verification |
| TC010 | View balance after credit | Balance modified by credit operation | 1. Perform credit operation<br>2. Select option 1<br>3. Observe balance | Display shows updated balance reflecting credit | TBD | TBD | Balance persistence after credit |
| TC011 | View balance after debit | Balance modified by debit operation | 1. Perform debit operation<br>2. Select option 1<br>3. Observe balance | Display shows updated balance reflecting debit | TBD | TBD | Balance persistence after debit |
| TC012 | Balance format validation | Any balance state | 1. Select option 1<br>2. Observe number format | Balance displays in format "XXXXXX.XX" with leading zeros | TBD | TBD | Data formatting consistency |

### Credit Account Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC013 | Credit account with valid amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "100.00"<br>3. Observe result | System displays "Amount credited. New balance: 001100.00" | TBD | TBD | Basic credit functionality |
| TC014 | Credit account with decimal amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "25.50"<br>3. Observe result | System displays "Amount credited. New balance: 001025.50" | TBD | TBD | Decimal handling |
| TC015 | Credit account with whole number | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "500"<br>3. Observe result | System displays "Amount credited. New balance: 001500.00" | TBD | TBD | Integer amount handling |
| TC016 | Credit account with maximum amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "999999.99"<br>3. Observe result | System processes if total ≤ 999999.99, otherwise handles overflow | TBD | TBD | Maximum limit testing |
| TC017 | Credit account with minimum amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "0.01"<br>3. Observe result | System displays "Amount credited. New balance: 001000.01" | TBD | TBD | Minimum amount validation |
| TC018 | Credit account with zero amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "0.00"<br>3. Observe result | System behavior depends on validation rules | TBD | TBD | Edge case - zero amount |
| TC019 | Credit account with negative amount | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "-50.00"<br>3. Observe result | System handles negative input appropriately | TBD | TBD | Invalid input handling |
| TC020 | Credit account with invalid format | Application running, balance = $1000.00 | 1. Select option 2<br>2. Enter "abc"<br>3. Observe result | System handles non-numeric input gracefully | TBD | TBD | Input validation |
| TC021 | Multiple consecutive credits | Application running, balance = $1000.00 | 1. Credit $100<br>2. Credit $200<br>3. Credit $50<br>4. Check balance | Final balance = $1350.00 | TBD | TBD | Multiple transaction handling |

### Debit Account Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC022 | Debit account with valid amount (sufficient funds) | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "100.00"<br>3. Observe result | System displays "Amount debited. New balance: 000900.00" | TBD | TBD | Basic debit functionality |
| TC023 | Debit account with exact balance amount | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "1000.00"<br>3. Observe result | System displays "Amount debited. New balance: 000000.00" | TBD | TBD | Exact balance debit |
| TC024 | Debit account with amount exceeding balance | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "1500.00"<br>3. Observe result | System displays "Insufficient funds for this debit." and balance unchanged | TBD | TBD | Overdraft protection |
| TC025 | Debit account with amount just over balance | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "1000.01"<br>3. Observe result | System displays "Insufficient funds for this debit." and balance unchanged | TBD | TBD | Precise overdraft validation |
| TC026 | Debit account with decimal amount | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "75.25"<br>3. Observe result | System displays "Amount debited. New balance: 000924.75" | TBD | TBD | Decimal handling in debit |
| TC027 | Debit account with minimum amount | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "0.01"<br>3. Observe result | System displays "Amount debited. New balance: 000999.99" | TBD | TBD | Minimum debit amount |
| TC028 | Debit account with zero amount | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "0.00"<br>3. Observe result | System behavior depends on validation rules | TBD | TBD | Edge case - zero debit |
| TC029 | Debit account with negative amount | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "-50.00"<br>3. Observe result | System handles negative input appropriately | TBD | TBD | Invalid input handling |
| TC030 | Debit account with invalid format | Application running, balance = $1000.00 | 1. Select option 3<br>2. Enter "xyz"<br>3. Observe result | System handles non-numeric input gracefully | TBD | TBD | Input validation |
| TC031 | Debit from zero balance | Application running, balance = $0.00 | 1. Select option 3<br>2. Enter "10.00"<br>3. Observe result | System displays "Insufficient funds for this debit." | TBD | TBD | Zero balance protection |
| TC032 | Multiple consecutive debits | Application running, balance = $1000.00 | 1. Debit $100<br>2. Debit $200<br>3. Debit $50<br>4. Check balance | Final balance = $650.00 | TBD | TBD | Multiple transaction handling |

### Data Persistence Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC033 | Balance persistence during session | Application running | 1. Credit $100<br>2. View balance<br>3. Debit $50<br>4. View balance | Balance correctly maintained: $1000→$1100→$1050 | TBD | TBD | Session data integrity |
| TC034 | Balance reset on application restart | Previous session with modified balance | 1. Exit application<br>2. Restart application<br>3. View balance | Balance resets to initial $1000.00 | TBD | TBD | No persistent storage |
| TC035 | Data consistency across operations | Application running | 1. Perform mixed operations<br>2. Check balance after each | Balance reflects all operations correctly | TBD | TBD | Data integrity validation |

### Integration and End-to-End Tests

| Test Case ID | Test Case Description | Pre-conditions | Test Steps | Expected Result | Actual Result | Status | Comments |
|--------------|----------------------|----------------|------------|-----------------|---------------|---------|----------|
| TC036 | Complete transaction workflow | Fresh application start | 1. Start app<br>2. View initial balance<br>3. Credit $500<br>4. View balance<br>5. Debit $200<br>6. View balance<br>7. Exit | Complete workflow executes without errors, final balance = $1300.00 | TBD | TBD | Full system integration |
| TC037 | Student account business rules | Application running | 1. Verify $1000 initial balance<br>2. Verify overdraft protection<br>3. Verify decimal precision | All student account rules enforced correctly | TBD | TBD | Business rule compliance |
| TC038 | Error recovery and continuation | Application running | 1. Trigger error condition<br>2. Continue with valid operations | System recovers gracefully and continues normal operation | TBD | TBD | Error handling robustness |
| TC039 | Maximum transaction limits | Application running | 1. Test maximum balance scenarios<br>2. Test maximum transaction amounts | System handles limits appropriately | TBD | TBD | System boundary testing |
| TC040 | Stress testing with multiple operations | Application running | 1. Perform 50+ mixed operations<br>2. Verify final balance calculation | System maintains accuracy throughout extended use | TBD | TBD | Performance and accuracy |

## Test Execution Instructions

1. **Setup**: Compile the COBOL application using: `cobc -x src/cobol/main.cob src/cobol/operations.cob src/cobol/data.cob -o accountsystem`
2. **Execution**: Run each test case systematically, recording results
3. **Documentation**: Update "Actual Result" and "Status" columns for each test
4. **Validation**: Review results with business stakeholders before Node.js migration

## Success Criteria

- **All menu navigation functions work correctly**
- **Balance inquiry displays accurate information**
- **Credit operations update balance correctly**
- **Debit operations enforce overdraft protection**
- **Data remains consistent during session**
- **Error handling prevents system crashes**
- **All business rules for student accounts are enforced**

## Notes for Node.js Migration

- Test cases can be directly translated to Jest/Mocha unit tests
- Business logic validation should remain identical
- Consider adding tests for persistent storage in Node.js version
- Input validation tests will be particularly important for web interface
- Error handling tests should be expanded for API responses

---

*This test plan covers the complete functionality of the COBOL Account Management System and serves as the foundation for both stakeholder validation and automated test creation during modernization.*
