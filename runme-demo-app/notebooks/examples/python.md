---
runme:
  id: 01HF7B0KJQ8625WYMCRVJADMQF
  version: v3
---

### Running Python Code

```python {"id":"01HWB12WZQXZQMXM8ZHC7P46QH","name":"python-datetime"}
import datetime

# Define a variable for the greeting
greeting = "Hello, World!"

# Get the current date and time
currentDateTime = datetime.datetime.now().strftime('%Y-%m-%d %H:%M:%S')

# Concatenate the greeting with the current date and time
fullGreeting = greeting + " It's now " + currentDateTime

# Output the full greeting
print(fullGreeting)
```
