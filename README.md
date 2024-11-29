# Fixing Background Colors in Terminal

## Step 1: Backup and Edit `dircolors`
1. **Backup the current `dircolors` configuration**:
   ```bash
   dircolors -p > ~/.dircolors
   ```

2. **Open the `.dircolors` file**:
   ```bash
   nano ~/.dircolors
   ```

3. **Edit entries with background colors**:
   Locate and edit the entries that include background color codes (like `42`, `41`, `44`, etc.) to use **only foreground colors**. For example:

   **Before**:
   ```plaintext
   DIR 01;34  # directory (no need to change this; it's fine)
   OTHER_WRITABLE 34;42  # directory with green background
   ```

   **After**:
   ```plaintext
   DIR 34  # directory (blue foreground)
   OTHER_WRITABLE 34  # directory with blue foreground, no background
   ```

4. **Key entries to fix**:
   - `OTHER_WRITABLE`: Remove `42`.
   - `STICKY_OTHER_WRITABLE`: Remove `42`.
   - `STICKY`: Remove `44`.
   - `SETUID` and `SETGID`: Remove `41` and `43`.
   - Any other entries with `40`, `41`, `42`, `43`, etc.

---

## Step 2: Apply the Updated `dircolors`
After saving the `.dircolors` file, apply the changes:
```bash
eval $(dircolors ~/.dircolors)
```

---

## Step 3: Test the Changes
Run the following command to test:
```bash
ls --color=auto
```
Verify that the background colors are removed.

---

## Step 4: Make the Changes Permanent
To make the changes persist across terminal sessions:

1. **Open your `.bashrc`**:
   ```bash
   nano ~/.bashrc
   ```

2. **Add the following line**:
   ```bash
   eval $(dircolors ~/.dircolors)
   ```

3. **Save and reload `.bashrc`**:
   ```bash
   source ~/.bashrc
   ```

---

## Final Notes
- **Foreground Only**: Ensure all `dircolors` entries specify **only foreground colors** (e.g., `01;34` for blue text).
- **Test Edge Cases**: Check directory permissions (sticky, writable, setuid) to ensure no background colors persist.
