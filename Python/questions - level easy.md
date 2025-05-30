**Q.1 Write a function called calc_discount that accepts two parameters. The first should be the full price of an item as an integer. The second should be the discount percentage as an integer.

The function should return the price of the item after the discount has been applied. For example, if the price is 50 and the discount is 20, the function should return 40.**
```python
def calc_discount(full_price, discount_percentage):
	discount_price = full_price * (discount_percentage / 100)
	return int(full_price - discount_price)

result = calc_discount(50, 20)
print(result)
```

**Q.2 The function reverse takes a string as input and returns that string in reverse order, with the opposite case.**
```python
def reverse(txt):
	new_str = ""
	for i in txt:
		if i.isupper():
			new_str = i.lower() + new_str
		else:
			new_str = i.upper() + new_str
	return new_str

#short trick: use [::-1].swapcase()
```
		
		