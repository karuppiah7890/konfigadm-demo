# konfigadm-demo

This is what I did to try out [konfigadm](https://github.com/flanksource/konfigadm)

```
$ # A vm with 2 CPUs
$ multipass launch -n konfigadm -c 2
$ multipass exec konfigadm bash
$ sudo wget -O /usr/bin/konfigadm https://github.com/flanksource/konfigadm/releases/download/v0.5.3/konfigadm
$ sudo chmod +x /usr/bin/konfigadm
$ konfigadm
$ # the below does a lot of installations!
$ sudo konfigadm apply -c - <<-EOF
kubernetes:
  version: 1.17.2
container_runtime:
  type: docker
commands:
  - kubeadm init
EOF
$ # and tada! Kubernetes was installed!! :D
$ mkdir -p $HOME/.kube
$ sudo cp -i /etc/kubernetes/admin.conf $HOME/.kube/config
$ sudo chown $(id -u):$(id -g) $HOME/.kube/config
$ # you can see the kub config file
$ cat ~/.kube/config
$ # connect to the cluster!
$ kubectl version
Client Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.2", GitCommit:"59603c6e503c87169aea6106f57b9f242f64df89", GitTreeState:"clean", BuildDate:"2020-01-18T23:30:10Z", GoVersion:"go1.13.5", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"17", GitVersion:"v1.17.2", GitCommit:"59603c6e503c87169aea6106f57b9f242f64df89", GitTreeState:"clean", BuildDate:"2020-01-18T23:22:30Z", GoVersion:"go1.13.5", Compiler:"gc", Platform:"linux/amd64"}
$ kubectl auth can-i create pod
yes
```