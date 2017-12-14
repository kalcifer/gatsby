---
title: How to contribute
---

## Filing an issue

If you want your issue to be resolved quickly, please include in your issue:

* Gatsby version, node.js version, OS version
* The contents of your `gatsby-config.js` and `package.json` as well as your
  `gatsby-node.js`, `gatsby-browser.js` `gatsby-ssr.js` files depending on
  changes you've made there.

## Contributing

Gatsby uses a "monorepo" pattern to manage its many dependencies and relies on
lerna and yarn to configure the repository for active development.

You can install the latest version of Gatsby by following these steps:

* Clone the repo, navigate to its directory.
* ensure you have the latest version of yarn installed (>= 1.0.2)
  https://yarnpkg.com/en/docs/install
* Install dependencies using `yarn run bootstrap` in the root of the repo.

The usual contributing steps are:

* Fork the [official repository](https://github.com/gatsbyjs/gatsby).
* Clone your fork: git clone `git@github.com:<your-username>/gatsby.git`
* setup up repo and Install dependencies: `yarn run bootstrap`
* Make sure tests are passing for you: `yarn test`
* Create a topic branch: `git checkout -b topics/new-feature-name`
* Run `npm run watch` from the root of the repo to first do an initial Babel
  build of all packages and then watch for changes to packages' source code and
  compile these changes on-the-fly as you work.
* Install [gatsby-dev-cli](/packages/gatsby-dev-cli/) globally: `yarn global add gatsby-dev-cli`
* For each of your Gatsby test sites, run the `gatsby-dev` command there to copy
  the built files from your cloned copy of Gatsby. It'll watch for your changes
  to Gatsby packages and copy them into the site. For more detailed instructions
  see the [gatsby-dev-cli README](/packages/gatsby-dev-cli/)
* Add tests and code for your changes.
* Once you're done, make sure all tests still pass: `yarn test`
* Commit and push to your fork.
* Create an pull request from your branch.

### Contributing to the documentation.

Gatsby, unsurprisingly uses Gatsby for it's documentation website. Here are the
steps to add/modify documentation and preview it.

* Clone the repo and navigate to `/www`
* Run `yarn` to install all of the website's dependencies.
* Run `gatsby develop` to preview the website in `http://localhost:8000`
* The Markdown files for the documentation live in `/docs` folder. Make
  additions or modifications here.
* Make sure to double check your grammar and capitalise correctly.
* Commit and push to your fork.
* Create an pull request from your branch.

## Development tools

### Redux devtools

Gatsby uses Redux for managing state during development and building. It's often
helpful to see the flow of actions and builtup state for a site you're working
on or if adding new functionality to core. We leverage
https://github.com/zalmoxisus/remote-redux-devtools and
https://github.com/zalmoxisus/remotedev-server to give you use the Redux
devtools extension for debugging Gatsby.

To use this, first install
[redux-devtools-extension](https://github.com/zalmoxisus/redux-devtools-extension)
in your browser. Then in your Gatsby repo, run `npm run remotedev`. Then in your
site directory run `REDUX_DEVTOOLS=true gatsby develop`. Depending on your
operating system and shell, you may need to modify how you set the
`REDUX_DEVTOOLS` environment variable.

At this point, your site will be sending Redux actions and state to the remote
server.

To connect to this, you need to setup the devtools extension to talk to the
remote server.

First open the remote devtools.

![how to open the redux remote devtools extension](./images/open-remote-dev-tools.png)

Then click settings along the bottom menu and set the host and port.

![how to set the host/port for the remote devtools extension to connect to Gatsby](./images/remote-dev-settings.png)

After this, the devtools extension _should_ connect to the remote server and
you'll see actions start showing up.

![gatsby redux remote devtools](./images/running-redux-devtools.png)

**Warning!! Lots of buginess**. While having this available is extremely
helpful, this setup is very buggy and fragile. There is a memory leak in the
extension that's triggered it seems every time you restart the Gatsby
development server. Also the extension often, for no apparent reason, just won't
show any actions from the remote server. It'll also often freeze up. The best
solution seems to just be turning everything off and on again. Fixing up these
tools would be very helpful for us and many others using these tools if someone
wants to take this on!
