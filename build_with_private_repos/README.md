# Building Docker image with private repository

Here you will find an example configuration on how to build a Docker image that will clone private repositories. In order for the example to work you have to complete a few steps prior to the build:

1. If not present already, create an ssh key for your computer. Recommended configuration will be:
    ```bash
    $ ssh-keygen -t rsa -b 4096 -C your_email@example.com
    ```
    and to select all default values. That should create `id_rsa` and `id_rsa.pub` under your `~/.ssh` folder.
2. Go to GitHub, and under your account settings, add your **public** key (i.e. `id_rsa.pub`) content under [SSH keys](https://github.com/settings/keys).
3. Copy your **private** key (i.e. `id_rsa`) into your repository. If you want the provided example to work, create a directory `.ssh` and place the private key in there as `private.pem`. **Note**: This private SSH key should *never* be committed. In the provided example, common SSH key names are included already in `.gitignore` to prevent this.
4. Finally, just go ahead and build the image, for example via:
   ```bash
   $ docker build -t myimage .
   ```
