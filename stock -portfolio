import requests
import json

# Replace 'YOUR_API_KEY' with your actual Alpha Vantage API key
API_KEY = 'YOUR_API_KEY'
BASE_URL = 'https://www.alphavantage.co/query'

class Portfolio:
    def __init__(self):
        self.stocks = {}

    def add_stock(self, symbol):
        if symbol in self.stocks:
            print(f"Stock '{symbol}' is already in the portfolio.")
            return
        self.stocks[symbol] = {'name': None, 'price': None}

    def remove_stock(self, symbol):
        if symbol in self.stocks:
            del self.stocks[symbol]
            print(f"Stock '{symbol}' removed from the portfolio.")
        else:
            print(f"Stock '{symbol}' not found in the portfolio.")

    def update_prices(self):
        for symbol in self.stocks:
            params = {
                'function': 'GLOBAL_QUOTE',
                'symbol': symbol,
                'apikey': API_KEY
            }
            response = requests.get(BASE_URL, params=params)
            if response.status_code == 200:
                data = response.json()
                if 'Global Quote' in data:
                    self.stocks[symbol]['price'] = float(data['Global Quote']['05. price'])

    def display_portfolio(self):
        print("\nCurrent Portfolio:")
        for symbol, info in self.stocks.items():
            print(f"{symbol}: {info['name']} - Price: ${info['price']}")

def main():
    portfolio = Portfolio()

    while True:
        print("\nMenu:")
        print("1. Add stock")
        print("2. Remove stock")
        print("3. Update prices")
        print("4. Display portfolio")
        print("5. Exit")

        choice = input("Enter your choice (1-5): ")

        if choice == '1':
            symbol = input("Enter stock symbol to add: ").strip().upper()
            portfolio.add_stock(symbol)
        elif choice == '2':
            symbol = input("Enter stock symbol to remove: ").strip().upper()
            portfolio.remove_stock(symbol)
        elif choice == '3':
            portfolio.update_prices()
            print("Prices updated.")
        elif choice == '4':
            portfolio.display_portfolio()
        elif choice == '5':
            print("Exiting program.")
            break
        else:
            print("Invalid choice. Please enter a number from 1 to 5.")

if __name__ == "__main__":
    main()
