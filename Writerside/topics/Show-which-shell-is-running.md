# Show which shell is running

Here are some examples of how you can find out which shell is running from the terminal:

1. **Using the `$SHELL` environment variable**:
   ```sh
   echo $SHELL
   ```

2. **Using the `ps` command**:
   ```sh
   ps -p $$
   ```

3. **Using the `echo` command with the `$0` parameter**:
   ```sh
   echo $0
   ```

4. **Using the `ps` command with the `-o` option**:
   ```sh
   ps -o comm= -p $$
   ```

These commands will help you identify the current shell you are using in your terminal.