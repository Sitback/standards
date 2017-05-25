# Sitback Standards() {

## Table of Contents

  1. [Coding Standards](#coding-standards)
  1. [Project Structure](#project-structure)
  1. [Version Control](#version-control)
  1. [Performance Goals](#performance-goals)
  1. [Supported Browsers, OS and Devices](#supported-targets)
  1. [Release Process](#release-process)

## Coding Standards

  > Coding standards describe how code must be written. All code should be
  > consistent and follow best practices so that it is easier to review 
  > and extend.

  <a name="coding-standards--tools"></a><a name="1.1"></a>
  - [1.1](#coding-standards--tools) **Tools**

    + EditorConfig: helps developers define and maintain consistent coding styles between different editors and IDEs. 
    + PHP_CodeSniffer: tokenizes PHP, JavaScript and CSS files and detects violations of a defined set of coding standards.
    + PHP_CodeSniffer Code Beautifier and Fixer: fixes many errors and warnings automatically.
    + ESLint: a tool to detect errors and potential problems in JavaScript code.
    + CSSLint: automated linting of Cascading Stylesheets
    + SASS Lint: a Node-only Sass linter for both sass and scss syntax!
    + Gulp: a toolkit that helps you automate painful or time-consuming tasks in your development workflow.
    + GrumPHP: automatically runs tests on the committed code. If the tests fail, the commit is rejected. 

  <a name="coding-standards--drupal"></a><a name="1.2"></a>
  - [1.2](#coding-standards--drupal) **Drupal**
  
    + Check that a PHP file conforms to Drupal coding standards
    + Check that a PHP file conforms to Drupal best practices
  
    ```phpcs --standard=Drupal $file```
    ```phpcs --standard=DrupalPractice $file```
  
  <a name="coding-standards--wordpress"></a><a name="1.3"></a>
  - [1.3](#coding-standards--wordpress) **WordPress**
  
    + Check that a PHP file conforms to Wordpress coding standards
  
    ```phpcs --standard=WordPress $file```  
    
  <a name="coding-standards--css"></a><a name="1.4"></a>
  - [1.4](#coding-standards--css) **CSS**
  
    + Check that a CSS file conforms to best practices
  
    ```csslint $file```  
      
  <a name="coding-standards--sass"></a><a name="1.5"></a>
  - [1.5](#coding-standards--sass) **SASS**
  
    + Check that a SASS file conforms to best practices
  
    ```sass-lint $file```
  
  <a name="coding-standards--js"></a><a name="1.6"></a>
  - [1.6](#coding-standards--js) **ECMAScript/JavaScript**
  
    + Check that a JS file conforms to best practices
  
    ```eslint $file```

## Project Structure

  > The boilerplate project structure attempts to simplify and standardise 
  > projects with the most common directory structures and files already 
  > included and set up.

  <a name="project-structure--boilerplate"></a><a name="2.1"></a>
  - [2.1](#project-structure--boilerplate) **Boilerplate**

  | Folder/File             | Description                               |
  | ----------------------- | ----------------------------------------- |
  | doc-root/               | Where your code base root should start.   |
  | results/                | This directory is just used to export test results to for parsing by external tools. |
  | scripts/                | A directory for project-specific scripts. |
  | tests/                  | A directory for external tests, such as selenium and phpunit. |
  | .dockerignore           | Contains a list of files to exclude from mounting/copying local files into a container. |
  | .gitignore              | Contains a list of the most common excluded files. |
  | bower.json              | Manifest of HTML, CSS, Javascript, fonts and even image component dependencies. |
  | ci-run.sh               | Shell script to run on continuous integration build to determine success or failure. |
  | docker-compose.ci.yml   | Docker compose file for running the continuous integration tests. |
  | Dockerfile.ci           | Dockerfile used to determine the continuous integration container. |
  | gulpfile.js             | Workflow automation script. |
  | package.json            | Manifest of node module dependencies. |
  | phpcs.xml               | Code sniffer configuration. |
  | README.md               | The project summary and changelog. |
  
## Version Control
  
  > GIT is the preferred source control repository. 
  > The methodology used is a modified gitflow method of using master, 
    develop, release and feature branches.
  
  There are at least two main branches: develop (or development)
  and master. There are also release, integration and feature branches 
  where new features are developed and tested. 
  
  Branches can span multiple releases. For example, feature branches are 
  sometimes not included in a release. This results in a long running 
  branch that needs to be kept in sync with the latest release. 
  
  The version control workflow is a way of maximising collaboration while
  minimising regression and loss of work caused by merge conflicts.
  
  <a name="version-control--branches"></a><a name="3.1"></a>
  - [3.1](#version-control--branches) **Branches**

  | Branch                  | Description                               |
  | ----------------------- | ----------------------------------------- |
  | master                  | Contains latest stable release that can be deployed to a production environment. This branch is purely a deployment branch and can be recreated if it becomes corrupted. |
  | develop                 | Contains latest stable release as well as project release history. |
  | release/x.x.x           | Contains all features for this release. | 
  | feature/u-[[ticket-nr]]-[[descriptive-name]] | Contains development work for a ticket. |
  | integration, aka deployment, such as 'staging' or 'qa' | Can contain multiple historic released merges. Ideally each integration branch would have its own deployment environment that gets recreated when all features are closed. These branches are used for CI builds and deployments for manual testing. |   
    
  <a name="version-control--workflow"></a><a name="3.2"></a>
  - [3.2](#version-control--workflow) **Workflow**

    + All work is done on a feature branch. 
    + Releases and features are branched off develop which is in sync 
      with the master, production deployment, branch.
    + Features are merged into a release branch and then merged into an
      integration, aka deployment, branch for testing.
    + Release are merged back into the develop branch with a tag after 
      all features are closed on the release branch. Then the develop 
      branch is merged into the master branch for deployment.
    + Hot fixes are treated as mini releases.
    
  <a name="version-control--separate-changes"></a><a name="3.3"></a>
  - [3.3](#version-control--separate-changes) **Separate Changes**

  > As a general rule, you should try to split your changes into small logical steps, and
  > commit each of them. They should be consistent, working independently 
  > of any later commits, pass the test suite, etc. This makes the review 
  > process much easier, and the history much more useful for later 
  > inspection and analysis, for example with git-blame(1) and git-bisect(1).
  
  To achieve this, try to split your work into small steps from the very beginning. It is
  always easier to squash a few commits together than to split one big commit into
  several. Don't be afraid of making too small or imperfect steps along 
  the way. You can always go back later and edit the commits with git 
  rebase --interactive before you publish them. You can use git stash 
  save --keep-index to run the test suite independent of other 
  uncommitted changes; see the EXAMPLES section of git-stash(1).

  <a name="version-control--managing-branches"></a><a name="3.4"></a>
  - [3.4](#version-control--managing-branches) **Managing Branches**
  
  > There are two main tools that can be used to include changes from one 
  > branch on another: git-merge(1) and git-cherry-pick(1). 

  Merges have many advantages, so we try to solve as many problems as 
  possible with merges alone. Cherry-picking is still occasionally useful; 
  see "Merging upwards" below for an example.
   
  Most importantly, merging works at the branch level, while cherry-picking 
  works at the commit level. This means that a merge can carry over the 
  changes from 1, 10, or 1000 commits with equal ease, which in turn means 
  the workflow scales much better to a large number of contributors (and contributions). 
  Merges are also easier to understand because a merge commit is a 
  "promise" that all changes from all its parents are now included. 

  <a name="version-control--graduation"></a><a name="3.5"></a>
  - [3.5](#version-control--graduation) **Graduation**
  
  As a given feature goes from experimental to stable, it also 
  "graduates" between the corresponding branches.
  Conceptually, the feature enters at an unstable branch, and 
  "graduates" to master for the next release once it is considered 
  stable enough.

  <a name="version-control--merging-upwards"></a><a name="3.6"></a>
  - [3.6](#version-control--merging-upwards) **Merging Upwards**
  
  The "downwards graduation" discussed above cannot be done by actually merging
  downwards, however, since that would merge all changes on the unstable 
  branch into the stable one.
  
  > Always commit your fixes to the oldest supported branch that require them. 
  > Then (periodically) merge the integration branches upwards into each other.

  <a name="version-control--feature-branches"></a><a name="3.7"></a>
  - [3.7](#version-control--feature-branches) **Feature Branches**
  
  Any nontrivial feature will require several patches to implement, and 
  may get extra bug-fixes or improvements during its lifetime.
  
  Committing everything directly on the integration branches leads to many problems: 
  Bad commits cannot be undone, so they must be reverted one by one, which creates 
  confusing histories and further error potential when you forget to revert part of 
  a group of changes. Working in parallel mixes up the changes, creating further confusion.
  
  Use of "feature branches" solves these problems. The name is pretty self explanatory,
  with a caveat that comes from the "merge upwards" rule above.

  <a name="version-control--merge-downstream"></a><a name="3.8"></a>
  - [3.8](#version-control--merge-downstream) **Merge Downstream**

  > Merge to downstream only at well-defined points.

  Do not merge to downstream except with a good reason: upstream API 
  changes affect your branch; your branch no longer merges to upstream cleanly; etc.

  Otherwise, the feature that was merged to suddenly contains more than a single
  (well-separated) change. The many resulting small merges will greatly clutter up
  history. Anyone who later investigates the history of a file will have to find out
  whether that merge affected the feature in development. An upstream might even
  inadvertently be merged into a "more stable" branch. And so on.

  <a name="version-control--deployment-branches"></a><a name="3.9"></a>
  - [3.9](#version-control--deployment-branches) **Deployment Branches**

  There will be many small feature branches, and during internal 
  testing you will need to merge and deploy them.

  > The solution, is to merge them into an release branch and then merge 
  > the result into an integration, aka deployment, branch.
  
  <a name="version-control--aggregate-branches"></a><a name="3.10"></a>
  - [3.10](#version-control--aggregate-branches) **Release Branches**

  > Release branches are used to integrate multiple feature branches and
  > minimise merge conflicts and pool all features for the release. 
  > Release branches are tested by being merged into a temporary 
  > deployment branch where CI tests are run and if they pass it is deployed.

  <a name="version-control--release-process"></a><a name="3.11"></a>
  - [3.11](#version-control--release-process) **Release Process**

    + Create a release branch from develop.
    + Create feature branches from develop.
    + Create integration branch from develop if it doesn't exist.
    + Graduate feature branches to the release branch after local tests pass.
    + Merge the release branch into an integration branch, deploy and manually test.
    + Once all feature branches pass integration tests the release is considered finalised.
    + Graduate the release branch to the develop branch and tag the release.
    + Merge the develop branch into the master branch and deploy to production/UAT.
    + Delete feature and release branches involved in this release.

## Performance Goals

  > A fast site is a good user experience (UX), and a satisfying UX 
  > leads to higher conversions. Slower page response time results in 
  > an increase in page abandonment. Page load also impacts Google 
  > search result scores - if response times are consistently over 2 
  > seconds then the number of indexed URLs is limited.

  There are 3 main time limits (which are determined by human perceptual 
  abilities) to keep in mind when optimizing web and application performance.
  
  The basic advice regarding response times has been about the same for 
  thirty years [Miller 1968; Card et al. 1991](https://www.nngroup.com/articles/response-times-3-important-limits/):
  
   * 0.1 second is about the limit for having the user feel that the system 
     is reacting instantaneously, meaning that no special feedback is 
     necessary except to display the result.
   * 1.0 second is about the limit for the user's flow of thought to stay 
     uninterrupted, even though the user will notice the delay. Normally, 
     no special feedback is necessary during delays of more than 0.1 but 
     less than 1.0 second, but the user does lose the feeling of operating 
     directly on the data.
   * 10 seconds is about the limit for keeping the user's attention 
     focused on the dialogue. For longer delays, users will want to perform 
     other tasks while waiting for the computer to finish, so they should 
     be given feedback indicating when the computer expects to be done. 
     Feedback during the delay is especially important if the response time 
     is likely to be highly variable, since users will then not know what 
     to expect.

<a name="performance-goals--rail"></a><a name="4.1"></a>
[4.1](#performance-goals--rail) **RAIL**

  + RAIL is a model for breaking down a user’s experience into key 
    actions (for example, tap, drag, scroll, load).
  + RAIL provides performance goals for these actions (for example, 
    tap to paint in under 100 milliseconds).
  + RAIL provides a structure for thinking about performance, so that 
    designers and developers can reliably target the highest-impact work.

<a name="performance-goals--rail--response"></a><a name="4.1.1"></a>
[4.1.1](#performance-goals--rail--response) **RESPONSE**

  If a user clicks on a button, you have to respond to their click before 
  they notice any lag. This applies to any input, really, whether it’s 
  toggling a form control or starting an animation. If it doesn’t happen 
  in a reasonable window of time, then the connection between action and 
  reaction breaks and the user will notice.

  Response is all about input latency: the lag between the finger touching 
  the glass and the resulting pixels hitting the screen. Have you ever 
  tapped on something and it took so long to respond that you started 
  wondering whether it registered your tap? That’s exactly the kind of 
  thing we want to avoid!

  Response’s primary interaction is:
  
   * tapping — when the user taps or clicks on a button or icon 
     (for example, tapping a menu icon to open off-screen navigation).

  To respond responsively, we would:
  
   * provide feedback in less than 100 milliseconds after initial input.
   * Ideally, the feedback would show the desired state. But if it’s going 
     to take a long time, then a loading indicator or coloring for the 
     active state will do. The main thing is to acknowledge the user so 
     that they don’t start wondering whether their tap was registered.

<a name="performance-goals--rail--animation"></a><a name="4.1.2"></a>
[4.1.2](#performance-goals--rail--animation) **ANIMATION**

  Animation is a pillar of modern apps, from scrolling to view transitions, 
  and we must be judicious with what we do in this period of time, 
  because the user will often be interacting directly and will really 
  notice if the frame rate varies. However, the user expects very smooth 
  feedback for more than what falls under the classic definition of animation.

  Animation includes the following:
  
   * Visual animation This includes entrance and exit animations, tweened 
     state changes, and loading indicators.
   * Scrolling This refers to when the user starts scrolling and lets go 
     and the page is flung.
   * Drag While we need to respond to the user’s interaction in 
     under 100 milliseconds, animation might follow as a result, as when 
     panning a map or pinching to zoom.

  To animate properly, each frame of animation should be completed in 
  less than 16 milliseconds, thereby achieving 60 FPS 
  (1 second ÷ 60 = 16.6 milliseconds).

<a name="performance-goals--rail--idle"></a><a name="4.1.3"></a>
[4.1.3](#performance-goals--rail--idle) **IDLE**

  Creating apps that respond and animate well often requires deferment 
  of work. The Optimistic UI patterns leverage this technique to great 
  effect. All sorts of work that must be completed likely does not need 
  to happen within a critical time window in the same way as “response” 
  or “load”: Bootstrapping the comments functionality, initializing 
  components, searching and sorting data, and beaconing back analytics 
  data are all non-essential items that we can do when the browser is idle.

  To use idle time wisely, the work is grouped into blocks of about 50 
  milliseconds. Why? Should a user begin interacting, we’ll want to 
  respond to them within the 100-millisecond response window, and not 
  be stuck in the middle of a 2-second template rendering.

<a name="performance-goals--rail--load"></a><a name="4.1.4"></a>
[4.1.4](#performance-goals--rail--load) **LOAD**

  Page-loading time is a well-trodden area of performance. We’re most 
  interested in getting the user to the first meaningful paint quickly. 
  Once that’s delivered, the app must remain responsive; the user must not 
  encounter trouble when scrolling, tapping or watching animations. 
  This can be super-challenging, especially when much of the work for a 
  page shares a single thread.
  
  To load pages quickly, we aim to deliver the first meaningful paint 
  in under 1 second. Beyond this, the user’s attention starts to wander 
  and the perception of dealing with the task at hand is broken. 
  Reaching this goal requires prioritizing the critical rendering path 
  and often deferring subsequent non-essential loads to periods of idle 
  time (or lazy-loading them on demand).
  
  Optimizing for performance is all about understanding what happens 
  in these intermediate steps between receiving the HTML, CSS, and 
  JavaScript bytes and the required processing to turn them into 
  rendered pixels - that’s the critical rendering path.
  
  Once the HTML content becomes available, the browser has to parse the 
  bytes, convert them into tokens, and build the DOM tree. 
  DevTools conveniently reports the time for DOMContentLoaded event, 
  which also corresponds to the blue vertical line. The gap between 
  the end of the HTML download and the blue vertical line 
  (DOMContentLoaded) is the time it took the browser to build the DOM tree.
  
  When we talk about the critical rendering path we are typically 
  talking about the HTML markup, CSS, and JavaScript. Images do not 
  block the initial render of the page. That said, the “load” event 
  (also commonly known as “onload”), is blocked on images. 
  The onload event marks the point when all resources required by the 
  page have been downloaded and processed - this is the point when the 
  loading spinner can stop spinning in the browser and this point is 
  marked by the red vertical line in the waterfall.
  
  Adding external CSS and JavaScript files added two extra requests to 
  our waterfall, all of which are dispatched at about the same time by 
  the browser - so far so good. However, note that there is now a much 
  smaller timing difference between the domContentLoaded and onload 
  events. What happened?
  
   * Unlike our plain HTML example, we now also need to fetch and parse 
     the CSS file to construct the CSSOM, and we know that we need both 
     the DOM and CSSOM to build the render tree.
   * Because we also have a parser blocking JavaScript file on our page, 
     the domContentLoaded event is blocked until the CSS file is downloaded 
     and parsed: the JavaScript may query the CSSOM, hence we must block 
     and wait for CSS before we can execute JavaScript.

  Inline scripts are parser blocking, but for external scripts we can 
  add the “async” keyword to unblock the parser.

<a name="supported-targets">
## Sitback supported browsers, OS and devices

  The criteria we use is 1% or more market share and the current version - 2 releases.

<a name="supported-targets--supported-browsers"></a><a name="5.1"></a>
[5.1](#supported-targets--supported-browsers) **Supported Browsers**

<table>
  <tr>
    <td>Browser</td>
    <td>Versions</td>
    <td>OS</td>
    <td>Comment</td>
  </tr>
  <tr>
    <td>Chrome</td>
    <td>56+</td>
    <td>Windows 7 SP1+
OSX
Android KitKat+
iOS 7+</td>
    <td>
    Chrome 56 has dropped to less than 1% as at May 2017 <br/>
Chrome 58 is current (Late May 2017)
</td>
  </tr>
  <tr>
    <td>Firefox</td>
    <td>52+</td>
    <td>Windows 7 SP1+
OSX
Android KitKat+
iOS 7+</td>
    <td>Firefox 50 has dropped to less than 1% as at March 2017<br/>
Firefox 53 is current (Late May 2017))</td>
  </tr>
  <tr>
    <td>Safari</td>
    <td>10+</td>
    <td>OSX
iOS 7+</td>
    <td>No Windows support for Safari. <br/> Safari 9.1 has dropped to  less than 1% as at April 2017</td>
  </tr>
  <tr>
    <td>IE</td>
    <td>11+</td>
    <td>Windows 7 SP1+</td>
    <td>IE11 is the only version to still be receiving even security updates</td>
  </tr>
  <tr>
    <td>Microsoft Edge</td>
    <td>14+</td>
    <td>Windows 10</td>
    <td>Version 14 is the only version greater than 1% usage in Australia</td>
  </tr>
</table>

<a name="supported-targets--supported-operating-systems"></a><a name="5.2"></a>
[5.2](#supported-targets--supported-operating-systems) **Supported Operating Systems**

<table>
  <tr>
    <td>OS</td>
    <td>Versions</td>
    <td>Comment</td>
  </tr>
  <tr>
    <td>Windows</td>
    <td>7 SP1+</td>
    <td>Extended Support for Windows7 SP1 ends Jan 14, 2020.</td>
  </tr>
  <tr>
    <td>OSX</td>
    <td>10.10+ (Yosemite, El Capitan, Sierra)</td>
    <td>This is the earliest version that has support for our supported Safari (9+).<br/>
All prior versions of the OS stop at Safari 9.</td>
  </tr>
  <tr>
    <td>iOS</td>
    <td>9+</td>
    <td>This includes 95% of IOS devices active in May 2017<br/>
https://developer.apple.com/support/app-store/</td>
  </tr>
  <tr>
    <td>Android</td>
    <td>KitKat+</td>
    <td>Accounts for 18% of Android users, but is now 7 versions old.<br/>
Android N is available, but currently only 7.1% of devices use it.<br/>
https://developer.android.com/about/dashboards/index.html</td>
  </tr>
</table>

<a name="supported-targets--supported-devices"></a><a name="5.3"></a>
[5.3](#supported-targets--supported-devices) **Supported Devices**

<table>
  <tr>
    <td>Device</td>
    <td>Comment</td>
  </tr>
  <tr>
    <td>Laptop</td>
    <td>13" and above</td>
  </tr>
  <tr>
    <td>Monitors</td>
    <td>13" and above</td>
  </tr>
  <tr>
    <td>iPad</td>
    <td>9.7" retina display</td>
  </tr>
  <tr>
    <td>iPad Mini</td>
    <td>7.9" retina display</td>
  </tr>
  <tr>
    <td>Android Tablets</td>
    <td>10" display</td>
  </tr>
  <tr>
    <td>iPod</td>
    <td>Touch</td>
  </tr>
  <tr>
    <td>Samsung Phone</td>
    <td>Galaxy S4 GT-19505</td>
  </tr>
  <tr>
    <td>Nokia Phone</td>
    <td>Lumia 520</td>
  </tr>
  <tr>
    <td>Samsung Phone</td>
    <td>Galaxy S4 GT-19505</td>
  </tr>
  <tr>
    <td>Nokia Phone</td>
    <td>Lumia 520</td>
  </tr>
  <tr>
    <td>Samsung Tablet</td>
    <td>Nexus 10</td>
  </tr>
  <tr>
    <td>Samsung Tablet</td>
    <td>GT-N8010 (Note)</td>
  </tr>
</table>

## Release process

The following process hopes to set a minimum set of release process to be inherited across all projects. It describes the process carried out for the staging and production environments, which should exists across most projects.

This process can be adapted for additional environments as required.


### Release feature to staging:
* Build feature
* Test feature on development environment
    * Run lint tests
    * Run unit tests (if any)
* Commit feature
* Merge feature to aggregate development branch
* Test feature on aggregate development branch
    * Run lint tests
    * Run unit tests (if any)
* Run integration tests (if any)
* Commit merged feature
* Merge aggregate development branch to deployment branch
* Commit deployment branch
* Push feature, merged feature and deployment branches
* Trigger continuous integration build
    * Build test environment
    * Run lint tests
    * Run unit tests (if any)
    * Run integration tests (if any)
    * Run behaviour tests (if any)
    * Deploy to staging environment
After the deployment, email project members that the deployment is complete and for the test team to conduct * feature and regression testing
* Test feature across supported browsers across devices
* Regression test business critical features across supported browsers across devices


### Release to production:
* Start a git flow release from the develop branch
* Tag the release
* Merge the aggregate development branch into the release branch
* Update the version and change log information
* Finish the release and delete the release branch
* Push the develop and master branches
* Create a release document with the commit hash and tag with change log information and save in Google Drive
* Before the release deployment, email all stakeholders when the deployment will start with the attached release document
* Start the release deployment script(s)
    * Create an instrumentation event
    * Run capistrano deploy task for production
* After the release is deployed, email all stakeholders that the deployment is complete and for the test team to conduct regression testing
* Regression test business critical features across supported browsers across devices

