## Steps to sign commits

### Step 1: Install GPG and Create a GPG Key Pair

- Go to [GPG Website](https://gnupg.org/download/index.html#binary) and choose the binary for your system and download it.
- Install the binary.
- Check if GPG is installed by running `gpg --version` in your terminal.
- Run the Kleopatra client or use terminal `gpg --full-generate-key` to generate a key pair.
- Create an RSA key with 4096 bits.
- Select appropriate expiry date for your key.
- Enter your name and email address.
- Enter a passphrase for your key. (OPTIONAL)
- Generate Key
- List key `gpg --list-secret-keys --keyid-format=long`
- This will list your keys. Copy the key ID of the key you want to use to sign commits. Key id is the string after rsa4096/ (in sec) and before the date.

### Step 2: Configure Git to Use GPG

- Copy the key id of the key you want to use to sign commits.
- `git config --global user.signingkey <key-id>`
- `git config --global commit.gpgsign true` This defaults to sign all your commit messages. Additionally, you can sign individual commits by passing the -S flag to the git commit command.
- `git config --global gpg.program <location of gpg.exe>` This tells git to use gpg program to sign commits. [IMPORTANT]
- For windows, location would be `C:\Program Files (x86)\GnuPG\bin\gpg.exe`, for linux, check the location of `gpg` binary using `which gpg` in your terminal, usually the location would be `/usr/bin/gpg`. 

### Step 3: Adding GPG Key to GitHub

- Export the key using `gpg --armor --export <key-id>` and copy the output. (Everything from ----Begin PGP PUBLIC KEY BLOCK---- to ----End PGP PUBLIC KEY BLOCK----)
- GO to GitHub settings and click on SSH and GPG keys.
- Click on New GPG Key.
- Paste the key and click on Add GPG Key.

And, voila! You can successfully sign your commits now.

You can commit and see your signature using `git log --show-signature`.

### References

- [GitHub Docs](https://docs.github.com/en/github/authenticating-to-github/managing-commit-signature-verification)
- [GPG Website](https://gnupg.org/download/index.html#binary)
- [GPG Tutorial](https://www.youtube.com/watch?v=3QnD2c4Xovk)
- [Common Error](https://stackoverflow.com/questions/36810467/git-commit-signing-failed-secret-key-not-available)
- [Blog](https://xebia.com/blog/why-you-should-start-signing-your-git-commits-today/#:~:text=By%20signing%20your%20commits%20you,the%20author%20of%20a%20commit.&text=This%20is%20not%20a%20security,real%20author%20of%20malicious%20code.)
- [Sign your previous commits](https://hyperledger-indy.readthedocs.io/projects/sdk/en/latest/docs/contributors/signing-commits.html)
