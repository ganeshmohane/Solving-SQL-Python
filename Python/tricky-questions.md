### Q.1 Return items from the list whom do not have repeated characters
```python
fruits = ['apple','orange','mango','kiwi']
for i in fruits:
    if len(set(i)) == len(i):
        print(i)
```
