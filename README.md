# personal_and_work_git_account
Record to setup two github in one user (Mac)


1. Generate a separate SSH key for each account:

ssh-keygen -t ed25519 -C "your_first_email@example.com" -f ~/.ssh/id_ed25519_first_account
ssh-keygen -t ed25519 -C "your_second_email@example.com" -f ~/.ssh/id_ed25519_second_account

2. Add public keys to your Git hosting accounts:
    2.1 copy your public key from [~/.ssh/id_ed25519_first_account.pub] or [~/.ssh/id_ed25519_second_account.pub]
    2.2 goto your github account:
        2.2.1 settings > SSH and GPG keys > New SSH key
        2.2.2 Input Title field and paste the content of your public key in to the Key field
            example :
                Title : My_first_account_SSH_key
                KeyType : Authentication Key
                Key : ssh-ed25519 [AXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXXX] [your_first_email@example.com]
        2.2.3 repeat the step to other github account

3. Configure your SSH client in (~/.ssh/config)
    3.1 Create or edit the config file
    # ~/.ssh/config

    # Configuration for your first account (e.g., personal)
    Host [myfirstgithub]
        HostName github.com
        User git
        IdentityFile ~/.ssh/[id_ed25519_first_account] # Path to your personal SSH key
        IdentitiesOnly yes 

    # Configuration for your second account (e.g., work)
    Host [github.com-work]
        HostName github.com
        User git
        IdentityFile ~/.ssh/[id_ed25519_work] # Path to your work SSH key
        IdentitiesOnly yes # Important: only use this specified key

4. Update your Git remote URLs:
    4.1 Navigate to your repository: 
        cd /path/to/your/project
    4.2 Change the remote URL:
        git remote set-url origin git@[myfirstgithub]:[your_first_github_username]/[your-repo.git]