# Push to Remotes

Just a simple hook to push code to remote forges from sourcehut

## Setting up 

The following steps will use jq filter notation to denote parts of the build manifest

### Setting up Sourcehut

- Generate an SSH key
    ```sh
    # Will generate a passwordless SSH key of type ed25519 into /tmp dir
    ssh-keygen -t ed25519 -f /tmp/id_ed25519 -N ""
    ```
- Add the private key to your sourcehut secrets
    - Copy your key
        ```sh
        cat /tmp/id_ed25519 | xclip -sel c
        ```
    - Go to https://builds.sr.ht/secrets and add the private key as an **SSH key**, optionally giving it a memorable name
    - Take note of the UUID 
- Add that UUID to your `.builds/push.yml` build manifest
- Update the `.sources` field in your build manifest

### Setting up Github

- Copy the public key from the keypair you generated earlier
    ```sh
    cat /tmp/id_ed25519.pub | xclip -sel c
    ```
- Add it as an SSH key to your account at https://github.com/settings/ssh/new
- Add the url under `.environment.github_url`

