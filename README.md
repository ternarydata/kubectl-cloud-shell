# Instructions for permanantly installing a current version of `kubectl` in Google Cloud Shell

Google Cloud Shell is a shell environment for managing resources hosted on Google Cloud Platform.
Cloud shell provides up to 5 GB of permanent user data storage, but the software virtual machine environment is
ephemeral - the machine resets once the shell has been shut down for 20 minutes. In the process, you lose any locally
installed software, unless you've installed it to your home directory.

`kubectl` is the default CLI tool for interacting with Kubernetes clusters. Cloud Shell comes with `kubectl` preinstalled
through the Google Cloud SDK, but the preinstalled version is quite old.

```
kubectl version
```

```
Client Version: version.Info{Major:"1", Minor:"10", GitVersion:"v1.10.7", GitCommit:"0c38c362511b20a098d7cd855f1314dad92c2780", GitTreeState:"clean", BuildDate:"2
018-08-20T10:09:03Z", GoVersion:"go1.9.3", Compiler:"gc", Platform:"linux/amd64"}
```

The current version of K8S is 1.13, so this can create problems with newer clusters;
compatibility is only guaranteed when K8S components are within one minor
version of each other. (https://kubernetes.io/docs/tasks/tools/install-kubectl/#before-you-begin)

These instructions are based on the
[instructions](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl)
for installing the `kubectl` Linux binary with cURL. First, open Cloud Shell and download the latest binary to your home
directory.

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```

Make the binary executable.

```
chmod +x ./kubectl
```

The next step in the basic instructions won't work beyond a single Cloud Shell session - `/usr/local/bin/` resets with
the Cloud Shell VM. However, cloud shell lets us install in our home directory in `~/bin/`. From your home directory,
create `~/bin/`:

```
mkdir bin
```

(Note that `~/bin/` will not be added to `$PATH` until we restart.)
Move the `kubectl` binary.

```
mv kubectl bin/
```

Now, reboot Cloud Shell and determine your `kubectl` version.

```
kubectl version
```

```
Client Version: version.Info{Major:"1", Minor:"13", GitVersion:"v1.13.1", GitCommit:"eec55b9ba98609a46fee712359c7b5b365bdd920", GitTreeState:"clean", BuildDate:"2
018-12-13T10:39:04Z", GoVersion:"go1.11.2", Compiler:"gc", Platform:"linux/amd64"}
```

You can install a particular version of `kubectl` rather than the latest by using cURL to download a specific binary
as shown [here](https://kubernetes.io/docs/tasks/tools/install-kubectl/#install-kubectl-binary-using-curl).
You can also switch between versions on the fly by placing a link in `~/bin/` pointing to the desired version.
