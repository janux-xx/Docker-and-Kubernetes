# T05-01 Using Kubernetes and Runing them

### Take you first lesson here:  [Kubernetes.io](https://kubernetes.io/docs/concepts/overview/) --> What is it; And What is not.

Let’s test our local Kubernetes installation.

    kubectl cluster-info

## Current context

Get the current context:

    kubectl config current-context

## List all contexts

List all the contexts:

    kubectl config get-contexts

## Change context

Use a context:

    kubectl config use-context [contextName]

## Using kubectx

What's great about Kubernetes is the incredible amount of tools created by the community and available for free.  Kubectx is a simple tool that provides an easy way to list and change context.

You can install it on:

Windows (if you have Chocolatey installed):

    choco install kubectx-ps

To list the contexts, simply type:

    kubectx

To change context:

    kubectx <contextName>

## Rename context

Rename context:

    kubectl config rename-context [old-name] [new-name]

## Delete context

Delete context:

    kubectl config delete-context [contextName]    