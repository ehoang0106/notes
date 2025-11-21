with `echo -e`:

```bash
echo -e "Hello\nWorld"
```

output: 

```bash
Hello
World
```

without `-e`:

```bash
echo "Hello\nWorld"
```

output:

```bash
Hello\nWorld
```


it is applying to color as well. For example

```bash
RED='\033[0;31m'

echo -e "${RED}Hello" #Output: Hello (with red color)

echo "${RED}Hello" #Output: \033[0;31mHello
```

