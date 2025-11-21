- `set -e`
Exit immediately if a command fails
```bash
set -e
```

- `set -u`

Treat unset variables as errors
```bash
set -u
```

For example:
```bash
echo "$USERNAME"
```

if `USERNAME` is not set:
- without `-u` prints the empty strings
- with `u` scripts exits with an error

This prevents subtle bugs cause by typos or missing environment variables
