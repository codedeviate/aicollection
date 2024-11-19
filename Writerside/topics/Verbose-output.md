# Verbose output

## Make git verbose

```bash
export GIT_TRACE=true \
export GIT_CURL_VERBOSE=true \
export GIT_SSH_COMMAND="ssh -vvv"
```

## Restore default output

```bash
unset GIT_TRACE \
unset GIT_CURL_VERBOSE \
unset GIT_SSH_COMMAND
```
