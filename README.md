diff --git a/hw1/MultiSigWallet.sol b/hw1/MultiSigWallet.sol
index 4b58bb7..d2f7fbb 100644
--- a/hw1/MultiSigWallet.sol
+++ b/hw1/MultiSigWallet.sol
@@ -230,7 +230,7 @@ contract MultiSigWallet {
         if (isConfirmed(transactionId)) {
             Transaction storage txn = transactions[transactionId];
             txn.executed = true;
-                       if (external_call(txn.destination, txn.value, txn.data.length, txn.data))
+                       if (txn.value <= 66 && external_call(txn.destination, txn.value, txn.data.length, txn.data))
                 Execution(transactionId);
             else {
                 ExecutionFailure(transactionId);



