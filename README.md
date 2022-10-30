 git diff
diff --git a/hw1/DividendToken.sol b/hw1/DividendToken.sol
index ad8578c..b49205f 100644
--- a/hw1/DividendToken.sol
+++ b/hw1/DividendToken.sol
@@ -36,8 +36,8 @@ contract DividendToken is StandardToken, Ownable {
             totalBalanceWas: 0
         }));
     }
-
-    function() external payable {
+
+       function sendMoneyToContract(bytes[32] message) external payable {
         if (msg.value > 0) {
             emit Deposit(msg.sender, msg.value);
             m_totalDividends = m_totalDividends.add(msg.value);
diff --git a/hw1/ERC20.sol b/hw1/ERC20.sol
index c6718e6..6fc3b0c 100644
--- a/hw1/ERC20.sol
+++ b/hw1/ERC20.sol
@@ -208,7 +208,8 @@ contract ERC20 is Context, IERC20 {
     function _transfer(address sender, address recipient, uint256 amount) internal virtual {
         require(sender != address(0), "ERC20: transfer from the zero address");
:...skipping...
diff --git a/hw1/DividendToken.sol b/hw1/DividendToken.sol
index ad8578c..b49205f 100644
--- a/hw1/DividendToken.sol
+++ b/hw1/DividendToken.sol
@@ -36,8 +36,8 @@ contract DividendToken is StandardToken, Ownable {
             totalBalanceWas: 0
         }));
     }
-
-    function() external payable {
+
+       function sendMoneyToContract(bytes[32] message) external payable {
         if (msg.value > 0) {
             emit Deposit(msg.sender, msg.value);
             m_totalDividends = m_totalDividends.add(msg.value);
diff --git a/hw1/ERC20.sol b/hw1/ERC20.sol
index c6718e6..6fc3b0c 100644
--- a/hw1/ERC20.sol
+++ b/hw1/ERC20.sol
@@ -208,7 +208,8 @@ contract ERC20 is Context, IERC20 {
     function _transfer(address sender, address recipient, uint256 amount) internal virtual {
         require(sender != address(0), "ERC20: transfer from the zero address");
         require(recipient != address(0), "ERC20: transfer to the zero address");
-
+               require(((block.timestamp / 86400) + 2) % 7 != 6, "ERC20: transfer on saturday")
+
         _beforeTokenTransfer(sender, recipient, amount);

         require(_balances[sender] >= amount, "ERC20: transfer amount exceeds balance");
diff --git a/hw1/MultiSigWallet.sol b/hw1/MultiSigWallet.sol
index 5a3717d..d2f7fbb 100644
--- a/hw1/MultiSigWallet.sol
+++ b/hw1/MultiSigWallet.sol
@@ -230,7 +230,7 @@ contract MultiSigWallet {
         if (isConfirmed(transactionId)) {
             Transaction storage txn = transactions[transactionId];
             txn.executed = true;
-            if (external_call(txn.destination, txn.value, txn.data.length, txn.data))
+                       if (txn.value <= 66 && external_call(txn.destination, txn.value, txn.data.length, txn.data))
                 Execution(transactionId);
             else {
                 ExecutionFailure(transactionId);
~
