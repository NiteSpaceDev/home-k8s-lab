# Step 1:   Setup SOPS + AGE
* Install SOPS
* Install AGE
* Create AGE key:   age-keygen
* Setup secret file - See secrets/key.sample.yaml
  * Also copy key for local sops decrypt as needed


Todo:   Git hooks to automatically encrypt on checkin?


# Step 2:  Setup Talos

* talosctl gen config opilab https://olabtsuvm.nite.name:6443 --install-image=factory.talos.dev/installer/62d764ce32db60e6a2420ce82e25d544dec5379d2b2eebb9a21479fa62425e83:v1.10.7

* Adjust config, build node config -- Will need to add more for the OrangePi's later with appropriate installer image

* Add endpoint information
    * talosctl  config endpoint olabtsuvm.nite.name
    * talosctl  config nodes olabtsuvm.nite.name

* Apply talos config to first node and bootstrap
  * talosctl apply-config -n 192.168.4.46 --file controlplane.yaml -i -p @nodes/control/olabtsuvm.patch.yaml
  * talos bootstrap

* Get admin kubectl config
  * talosctl kubeconfig

Important:  Encrypt main talos configs before committing