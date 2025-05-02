import hashlib
import secrets

class BitcoinWallet:
    def __init__(self, owner):
        self.owner = owner
        self.balance = 0.0  # بیت‌کوین فرضی
        self.transactions = []
        self.private_key = secrets.token_hex(32)  # تولید کلید خصوصی تصادفی
        self.public_key = hashlib.sha256(self.private_key.encode()).hexdigest()  # تولید کلید عمومی

    def deposit(self, amount):
        if amount > 0:
            self.balance += amount
            self.transactions.append(f"Deposited {amount} BTC")
            return f"{amount} BTC added to wallet. New balance: {self.balance} BTC"
        return "Invalid amount!"

    def withdraw(self, amount):
        if 0 < amount <= self.balance:
            self.balance -= amount
            self.transactions.append(f"Withdrew {amount} BTC")
            return f"{amount} BTC withdrawn. New balance: {self.balance} BTC"
        return "Insufficient balance or invalid amount!"

    def show_transactions(self):
        return "\n".join(self.transactions)

    def show_keys(self):
        return f"🔒 Private Key: {self.private_key}\n🔑 Public Key: {self.public_key}"

# نمونه استفاده
my_wallet = BitcoinWallet("Abtin")
print(my_wallet.deposit(2.0))  # افزودن بیت‌کوین فرضی
print(my_wallet.withdraw(0.8))  # برداشت بیت‌کوین فرضی
print("Transaction History:\n", my_wallet.show_transactions())
print(my_wallet.show_keys())  # نمایش کلیدهای خصوصی و عمومی
