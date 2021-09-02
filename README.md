# kube-aliases

kube-aliases comes with a comprehensive set of aliases for Kubernetes. If
desired, there is a utility tool to generate custom aliases or to change the
aliases automatically. For example, if you prefer `rm` to `del` for deleting.

[Usage](# Usage)
    [General Alias Rules](## General Alias Rules)
    [Generating Aliases](## Generating Aliases)
        [Customizing Aliases](### Customizing Aliases)
            [resources](#### resources)
            [additional](#### additional)
[Installation](# Installation)
    [Bash Example](## Bash Example)
    [Zsh Example](## Zsh Example)
    [Generate Aliases](## Generate Aliases)
    [AUR](## AUR)
    
# Usage

## General Alias Rules

Aliases follow the following conventions:

```bash
k           # kubectl
kc<r>       # kubectl create <resource>, e.g. kcd for kubectl create deployment
kdel<r>     # kubectl delete <resource>, e.g. kdelp for kubectl delete pods
kd<r>       # kubectl describe <resource>, e.g. kdp for kubectl describe pod
ke<r>       # kubectl edit <resource>, e.g. kep for kubectl edit pods
kg<r>       # kubectl get <resource>, e.g. kgp for kubectl get pods
kga<r>      # kubectl get --all-namespaces -o wide <resource>, e.g. kgap for kubectl --all-namespaces -o wide get pods
```

## Generating Aliases

Want to generate custom aliases? Install the latest `generate-kube-aliases`
from releases. Using our `aliases.yaml` file as a base run

```bash
generate-kube-aliases aliases.yaml ~/.aliases
```

Then the aliases can be sourced 
```bash
source ${HOME}/.aliases
```

### Customizing Aliases

To easily customize the generated aliases, download `generate-kube-aliases` to
your any of your bins. See [installation](## Generate Aliases).

#### resources

Resources defines Kubernetes resources and what the short letter representation
should be.

```yaml
resources:
  <resource>:
    short: <short name>
```

For example

```yaml
resources:
  pods:
    short: p
```

Which will generate aliases `alias k<cmd>p=kubectl <cmd> pod`.

####  cmds

`cmd` will generate the main command on all resources.

```yaml
cmd:
  - short: <short name>
    cmd: <cmd>
    # Optional
    prefix:
      short: <short name>
      cmd: <cmd>
    # Optional
    suffix:
      short: <short name>
      cmd: <cmd>
```

For example:

```yaml
cmd:
  - short: g
    cmd: get
```

Will generate aliases for get commands for each specified resource in the
format `alias kg<resource>=kubectl get <resource>`.  An example with the `pod`
resource is `alias kgp=kubectl get pod`.  Prefix and suffix will generate
commands before and after the alias respectively.

Prefix example that will generate `alias wkg<resource short>=watch kubectl get <resource>`.

```yaml
  - short: g
    cmd: get
    prefix:
      short: w
      cmd: watch
```


#### additional

Any other aliases can be generated by the following

```yaml
additional:
  - short <short>
    cmd: <cmd>
```

The following will generate `alias eh="echo hello"`

```yaml
additional:
  - short eh
    cmd: "echo hello"
```

# Installation

To simply grab a bunch of aliases without customization simply get the
`aliases` file and source it in your `bashrc` or `zshrc` file.

## Bash Example

```bash
curl https://raw.githubusercontent.com/Dbz/kube-aliases/master/aliases -o ${HOME}/.kube-aliases
echo "source ${HOME}/.kube-aliases" >> .bashrc
```

## Zsh Example

```bash
curl https://raw.githubusercontent.com/Dbz/kube-aliases/master/aliases -o ${HOME}/.kube-aliases
echo "source ${HOME}/.kube-aliases" >> .zshrc
```

## Generate Aliases

Coming soon

## AUR

Coming soon

