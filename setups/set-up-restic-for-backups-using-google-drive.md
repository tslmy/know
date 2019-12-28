# Set up Restic for backups using Google Drive

Although official documentation instructed to use `curl https://rclone.org/install.sh | sudo bash` for installing `rclone`, since `rclone` is available view `brew`, I figured that I'll use `brew` instead, for the sake of mroe centralized storage.

```bash
brew install rclone restic
rclone config
```

We need to configure Google Drive to work with `rclone`. This can be done by following the official instructions found [here](https://rclone.org/drive/#making-your-own-client-id):

> 1. Log into the [Google API Console](https://console.developers.google.com/) with your Google account. It doesn’t matter what Google account you use. **\(It need not be the same account as the Google Drive you want to access\)**
> 2. Select a project or create a new project.
> 3. Under “ENABLE APIS AND SERVICES” \[...\] enable the “Google Drive API”.
> 4. Click “Credentials” in the left-side panel \(not “Create credentials”, which opens the wizard\), then “Create credentials”, then “OAuth client ID”. It will prompt you to **set the OAuth consent screen product name, if you haven’t set one already.**

You must configure your OAuth consent screen in order to see the OAuth option in Step 4. This is very important.

> 1. Choose an application type of “other”, and click “Create”. \(the default name is fine\)
> 2. It will show you a client ID and client secret. \[...\]

Now connect `rclone` to this API, following [this](https://rclone.org/drive/) doc. The following optional settings are worth noticing:

* Since we are going to encrypt our backups anyways, it makes little sense to use the "Computers" folders on Google Drive.
* Leave Service Account Credentials blank. This will have the effect that `rclone` require you to authorize the Google account whose Drive you want to save backups to. This can be a separate account than the one you configured the Google Cloud project with. Don't user Auto Config -- it didn't work for me on my MacBook at least.
* Don't set a password for the `rclone` config file.

Now you can quit `rcloud config`. Issue the following command to let `restic` talk to `rcloud`:

```bash
restic -r rclone:[rcloud config name]:restic-backups/macbook/ init
```

Use a strong password.

Initiate your first backup with:

```bash
restic -r rclone:[rcloud config name]:restic-backups/macbook/ backup ~/Backups
```

After a backup, you should be able to mount the storage to a local directory:

```text
brew cask install osxfuse # if you haven't done this already
restic -r rclone:[rcloud config name]:restic-backups/macbook/ mount ~/mnt
```

