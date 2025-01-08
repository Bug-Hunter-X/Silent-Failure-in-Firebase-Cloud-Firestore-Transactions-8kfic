# Silent Failure in Firebase Cloud Firestore Transactions

This repository demonstrates a subtle bug in Firebase Cloud Firestore transactions where exceptions thrown within the transaction callback are not properly handled, leading to silent failures. The application may believe the transaction succeeded, while the database remains unchanged.

The `transactionBug.js` file contains code that reproduces the issue.  `transactionSolution.js` provides a corrected version with improved error handling.

## How to Reproduce

1.  Ensure you have the Firebase JavaScript SDK installed and configured.
2.  Run `transactionBug.js`. Observe that despite the error, the application indicates success.
3.  Verify the state of your Firestore document to confirm that no changes have been made.
4.  Run `transactionSolution.js` to see the corrected behaviour.

## Root Cause and Solution

The root cause is the lack of comprehensive error handling within the transaction callback.  The solution involves carefully handling any potential exceptions within the callback, either by retrying the transaction or gracefully reporting the failure to the user.  The improved example uses a `try...catch` block and properly propagates the error.