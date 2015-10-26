# Running the latest (4.2.x) LTS Node[.js] version on Red Hat's OpenShift PaaS
This git repository is a sample Node application along with the "orchestration" bits to help you run the latest (or a custom) version of Node on Red Hat's OpenShift PaaS.

(Current) NodeJS Version: 4.2.1

## Steps to get the latest Node.js version running on OpenShift
Create an account at [http://openshift.redhat.com/](http://openshift.redhat.com/)

Create a namespace, if you haven't already do so

```
rhc domain create <yournamespace>
```

Create a nodejs application (you can name it anything via -a, -t here is   used to start with the default supported OpenShift nodejs application)

```
rhc app create -a node4  -t nodejs-0.10
```

Add this `github nodejs-4-lts-openshift` repository to the OpenShift git project remote

```
cd node4
git remote add github -m master https://github.com/h4t0n/nodejs-4-lts-openshift.git
```

Get updates from the remote with merge conflicts properly resolved (NB: don't run `git pull github` alone)     

```
git pull -s recursive -X theirs github master
```

Push the updates coming from `github nodejs-4-lts-openshift` into the OpenShift git project.

```
git push
```

That's it, you can now checkout your application at:

  [http://node4-$yournamespace.rhcloud.com](http://node4-$yournamespace.rhcloud.com)
  ( See env @ [http://node-$yournamespace.rhcloud.com/env](http://node-$yournamespace.rhcloud.com/env) )

If you want another version of Node (example v0.12.x), you can change to that by just writing it to the end of the NODEJS_VERSION file and committing that change.

```
echo 0.12.7 >> .openshift/markers/NODEJS_VERSION
#
# Or alternatively, edit the .openshift/markers/NODEJS_VERSION file
# in your favorite editor aka vi ;^)
#
#
git commit . -m 'use Node version 0.12.7'
```

Then push the repo to OpenShift with `git push`

## Additional information
This repository is a fork of [Ramr nodejs custom version](https://github.com/ramr/nodejs-custom-version-openshift). See it for documentation about Openshift hooks or if you want additional information.
