# ✅Pydantic

is a Python library that helps you create **data models** easily.
It checks that your data has the **right types and values** — **at runtime** (while your code runs).
You define classes with fields and their types, and Pydantic makes sure the data fits those types.
If the data is wrong, Pydantic gives a **clear error message**.

# Example:

```python
from pydantic import BaseModel

class User(BaseModel):
    name: str
    age: int

user = User(name="Alice", age=25)  # OK
user = User(name="Bob", age="twenty")  # Error: age must be int
```

# Why use Pydantic?

* It saves you from writing manual checks.
* It makes your code safer and cleaner.
* It’s used in popular tools like **FastAPI**.