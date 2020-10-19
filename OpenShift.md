# Red Hat OpenShift.

```
oc version
```
```
[ ! -d 'cc201' ] && git clone https://gitlab.com/ibm/skills-network/courses/cc201.git

cd cc201/labs/4_IntroOpenShift/
```
```
oc get pods
```
In addition to Kubernetes objects, you can get OpenShift specific objects.
```
oc get buildconfigs
```
View the OpenShift project that is currently in use.
```
oc project
```

Click the outer circle to get information on the application.
Click the inner circle with the Node.js logo to get information on the Deployment.
Click the GitHub icon to access the code repository.
Click the check mark to view the most recent build (you will see circular arrows if the build is in progress).
Click the arrow coming out of a box to view the application in the browser if the application is externally available.

1- Click the inner circle with the Node.js logo to bring up information on the Deployment.

2- Observe the four resources associated with this Deployment: a Pod that runs the containerized application; a Build that uses the s2i strategy to build the application into a container image; a Service that exposes the application as a network service; and a Route that provides an externally reachable hostname.

3- Click View logs on the line that says Build #1.

4- Read the logs to see a few key completed steps. The repository is cloned, a Dockerfile is generated, an image is built, and the image is pushed to the internal registry.

5- Click the Overview tab for this Build.

6- Click the link to the owning BuildConfig under Owner.

7- If you look at the Overview and YAML tabs, you'll see many concepts that we talked about in this module: triggers, build strategy, webhooks, and more.

8- From the Overview tab, click the link to the ImageStreamTag under Output To.

9- You can now see the ImageStreamTag that was created as an output of the build. Click the History tab to see the image in the internal registry to which this ImageStreamTag points.

10- Return to the Topology view and click on your Deployment info. Click the Route that OpenShift automatically created for you. This will open the application in the browser.
#####################################################################################################

One way to accomplish this automation is by using continuous integration and continuous
delivery, or CI/CD.
This method automates the building, testing, and merging of new code changes, as well as
the release of those changes to a repository and their deployment to environments.
Red Hat OpenShift provides CI/CD capabilities out of the box.

In OpenShift, a build is simply the process of transforming inputs into a resultant object.

A **build configuration**, or **BuildConfig**, is an OpenShift-specific object that defines
the process for a build to follow.
So the BuildConfig is the blueprint, and the build is an instance of that blueprint put
into action.
OpenShift builds can automate the build process that we performed in our earlier modules.
Given a repository that contains a Dockerfile and the necessary artifacts, OpenShift invokes
the “docker build“ command to create an image, just as we did from the command line.
Thus, when a build is kicked off, OpenShift will take the input and produce a resultant
image, pushing it to the internal OpenShift registry.
In OpenShift, this strategy is simply called "Docker."
## "Source-to-image"
is another build strategy offered by OpenShift.
Source-to-image, often abbreviated as "s2i," is a tool for building reproducible container
images.
S2i injects application source code into a container image to produce a ready-to-run
image.
The new image is built by incorporating a builder image and the source.
This eliminates the need to write a Dockerfile and lets you go from source to image in a
single step; hence the name.
This valuable optimization saves time and development effort.
OpenShift comes with a variety of builder images available.
Finally, a custom build represents a more advanced strategy.
Here, you must define a builder image that will be used for the build process, rather
than relying on a builder image provided by OpenShift.
Customer builder images are regular Docker images that contain the logic needed to transform
the inputs into the expected output.
Both the Docker and s2i strategies result in runnable images, but the custom build strategy
can be used to create any resulting objects.
These can be .jar files or Python packages, for example.
Let’s look at a sample configuration file for a BuildConfig.
This is similar to the Deployment files we saw in earlier modules, but this sample will
create a BuildConfig in OpenShift.
There are some new BuildConfig-specific fields for us to note.
The output field shows us what a build using this configuration will produce.
In this case, it will produce an ImageStreamTag, with repo name “example” and tag “latest”.
We’ll talk about ImageStreams shortly.
The strategy field indicates the build strategy, which in this case is source-to-image, using
a Node.js builder image.
The source is a git repository where the source for this build is located.
The triggers describe events that can automatically cause a build to run.
While you can run builds manually in OpenShift, this process can and should be automated.
There are three build triggers available that stipulate when a build should run.
The first is **webhook triggers.**
## webhook
A webhook sends a request to an OpenShift Container Platform API endpoint.
Often this will be a GitHub webhook, though it can also be a generic webhook.
If a GitHub webhook is utilized, GitHub can send the request to OpenShift when there is
a new commit on a certain branch, when a pull request is merged, and under many more circumstances.
Webhooks are a great way to automate development flows so that builds can occur automatically
as new code is developed.
The second trigger is image change.
In this scenario, builds can be triggered when a new version of an image is available.
For example, if your application is built using a Node.js base image, that image will
be updated as security fixes are released and other updates occur.
You can automate a build to rebuild your containerized applications when base images are updated
so that your code always contains the latest security fixes.
Lastly, the configuration change trigger causes a new build to run when a new BuildConfig
resource is created.
We mentioned that the output for our example build would result in an ImageStreamTag.
## ImageStreams 
are a nifty way to represent images in OpenShift.
An ImageStream is an abstraction for referencing images within OpenShift.
Let’s say you store your images in IBM Cloud Container Registry, and you push an image
to your repo using the tag “latest.”
You can push another image to that repo and use the ”latest” tag again, which will
remove it from your first image.
If your Deployments were referring to images by repo and tag, they would now start pulling
the new image, but that could be unintended.
Each image also contains an ID, or digest, that identifies it.
While tags can change, the digest will not.
ImageStreams do not contain image data but are pointers to image digests.
Therefore, even if a new image is pushed with the same tag, Deployments referencing the
ImageStream will not be changed until the ImageStream is updated to point to the new
image.
The source images that ImageStreams point to can be stored in the internal registry,
external registries, or other ImageStreams.
You should now be familiar with OpenShift builds and BuildConfigs and what makes them
different.
You should also understand the various build strategies and triggers offered by OpenShift,
as well as how ImageStreams are used to create virtual repositories of images.
