# Setup the environment

1. Install multipass
   The fist step is to install multipass, a lightweight VM manager for Linux, Windows, and macOS.

   ```shell
   sudo snap install multipass --classic
   ```

2. Create a virtual machine

   ```shell
   multipass launch --name k3s --cpus 2 --mem 8G --disk 40G
   ```
   Mount the home into the vm:
   ```shell
   multipass mount $HOME k3s
   ```
   
   You can check your instance with the following command:
   ```shell
   multipass info k3s
   ```

   You can check the status of the VM with the following command:

   ```shell
   multipass list
   ```
   The output should be similar to this:

   ```shell
   Name                    State             IPv4              Image
   k3s                     Running           ***.***.***.***   Ubuntu 20.04 LTS
   ...                     ...               ...               ... 
   ```
   The displayed IP is important, because it's the way for us to access our cluster. K3s come per default with traefik
   ingress controller.

   You can now enter your vm by doing
   ```shell
   multipass shell k3s
   ```

3. Install K3s

   ```shell
   curl -sfL https://get.k3s.io | sh -
   ```

4. Install Helm
   ```shell
   curl -fsSL -o get_helm.sh https://raw.githubusercontent.com/helm/helm/master/scripts/get-helm-3
   chmod 700 get_helm.sh
   ./get_helm.sh
   ```

5. (Optional) Install [k9s](https://k9scli.io/) into the VM
   ```shell
   curl -sS https://webinstall.dev/k9s | sh
   ```

6. (Optional) Alias kubectl and helm from the virtual machine

   **_Do this in another shell, on your host machine._**

   Add these lines to your shell configuration file (e.g., `~/.bashrc` or `~/.zshrc`):
   ```shell
   alias kubectl='multipass exec k3s -- sudo kubectl'
   alias helm='multipass exec k3s -- helm'
   ```

   Then, reload your shell configuration file:
    ```shell
   source ~/.bashrc
   ```
   
7. Test the whole installation, from your host machine
   ```shell
   kubectl version
   helm version
   ```
