
1. Register Account Name – input and confirmation
2. Deposit Amount – update balance
3. Withdraw Amount – update balance
4. Record Exchange Rate – select currency, input rate
5. Currency Exchange – source currency, amount, converted amount
6. Show Interest Computation – table of daily balances and interest

---
**TODO LIST
- [x] Account Name Registration
- [x] Deposit Amount
- [x] Withdraw Amount
- [ ] Record Exchange Rate
- [ ] Currency Exchange
- [ ] Interest Computation Display

---
# Conversions

```
	rates[Currency::PHP.get_index()] = 1.0;
	rates[Currency::USD.get_index()] = 58.15;
	rates[Currency::JPY.get_index()] = 0.39;
	rates[Currency::GBP.get_index()] = 78.04;
	rates[Currency::EUR.get_index()] = 67.79;
	rates[Currency::CNY.get_index()] = 8.15;
```

PHP -> USD = `1.0 * 58.15`
PHP -> JPY = ``
