diff --git a/hw1/ERC20.sol b/hw1/ERC20.sol
index c6718e6..d070d06 100644
--- a/hw1/ERC20.sol
+++ b/hw1/ERC20.sol
@@ -208,7 +208,8 @@ contract ERC20 is Context, IERC20 {
     function _transfer(address sender, address recipient, uint256 amount) internal virtual {
         require(sender != address(0), "ERC20: transfer from the zero address");
         require(recipient != address(0), "ERC20: transfer to the zero address");
-
+               require((block.timestamp / 86400) % 7 != 6, "ERC20: transfer on saturday")
+
         _beforeTokenTransfer(sender, recipient, amount);

         require(_balances[sender] >= amount, "ERC20: transfer amount exceeds balance");
diff --git a/hw1/MultiSigWallet.sol b/hw1/MultiSigWallet.sol
index 4b58bb7..d2f7fbb 100644
--- a/hw1/MultiSigWallet.sol
+++ b/hw1/MultiSigWallet.sol
@@ -230,7 +230,7 @@ contract MultiSigWallet {
:...skipping...
diff --git a/hw1/ERC20.sol b/hw1/ERC20.sol
index c6718e6..d070d06 100644
--- a/hw1/ERC20.sol
+++ b/hw1/ERC20.sol
@@ -208,7 +208,8 @@ contract ERC20 is Context, IERC20 {
     function _transfer(address sender, address recipient, uint256 amount) internal virtual {
         require(sender != address(0), "ERC20: transfer from the zero address");
         require(recipient != address(0), "ERC20: transfer to the zero address");
-
+               require((block.timestamp / 86400) % 7 != 6, "ERC20: transfer on saturday")
+
         _beforeTokenTransfer(sender, recipient, amount);

         require(_balances[sender] >= amount, "ERC20: transfer amount exceeds balance");
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
