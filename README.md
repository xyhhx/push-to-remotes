# Push to Remotes

Just a simple hook to push code to remote forges from sourcehut

## Setting up 

The following steps will use jq filter notation to denote parts of the build manifest

This build process uses personal access tokens instead of SSH keys. The reasoning is that SSH keys give unfettered access to all repos that your account can write to, whereas a personal access token can be restricted somewhat. The actual restrictions that can be applied will vary depending on which forge you're referring to, but we'll cover the popular ones here.

### Setting up Github

1. Generate a personal access token on Github
    - Go to https://github.com/settings/personal-access-tokens/new 
    - Give it a descriptive name that includes the repo's name 
    - Select *Only select repositories*, and choose the repo you want to push to
    - Give it **read and write** access to *Contents*
    - Copy the generated token, obviously
1. Add the generated token to your sourcehut secrets dashboard
    - Go to https://builds.sr.ht/secrets
    - Give the secret a descriptive name. I like to call it "<repo name> github PAT" (where `<repo name>` is the name of the repository you're mirroring)
    - Paste the token into the secret's value
    - Select **File** as the *Secret type*
    - For path, choose `~/secrets/github_pat`
    - Just to be safe, set a mode of `600`
    - Click *Add secret*, and take note of its UUID
1. Update the build manifest
    - Add the UUID for your Github PAT to your `.secrets` list
    - Populate the `.environment.github_username` and `.environment.github_repo` variables
        - (The repo is off the format `user/repo` only)

### Setting up any Forgejo or Gitea

These instructions are almost identical to Github, except for generating the personal access token.
We'll use https://codeberg.org as the example here, but this should work for any Forgejo or
Gitea instance.

1. General a personal access token
    - Go to https://codeberg.org/user/settings/applications 
    - Around the top, under *Generate new token*, add a descriptive name
    - You can select *All (public, private, and limited)* or *Public only*
    - Under *Select permissions*, give it **Read and write** access to *repository*
    - Hit *Generate token*
    - Copy the generated token, of course
1. Add the generated token to your sourcehut secrets dashboard
    - Go to https://builds.sr.ht/secrets
    - Give the secret a descriptive name. I like to call it "Codeberg PAT" (no need to mention any repo, since this PAT can push to any repo you have access to)
    - Paste the token into the secret's value
    - Select **File** as the *Secret type*
    - For path, choose `~/secrets/codeberg_pat`
    - Just to be safe, set a mode of `600`
    - Click *Add secret*, and take note of its UUID
1. Update the build manifest
    - Add the UUID for your Codeberg PAT to your `.secrets` list
    - Populate the `.environment.codeberg_username` and `.environment.codeberg_repo` variables
        - (The repo is off the format `user/repo` only)
