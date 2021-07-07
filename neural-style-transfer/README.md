# Neural Style Transfer

Neural style transfer is an algorithmic technique for taking the "style" of one digital image and applying it to the "content" of another. In this workshop, we will focus on the use of neural style transfer in creative art practice by generating images in [RunwayML](https://runwayml.com/), out-of-the-box software that lets you apply style transfer techniques to your own images.

This workshop is designed for participants who are new to neural style transfer. No computer programming experience is required.

## Art & AI

### Key Terminology
- **artificial intelligence** - used to describe computer programs that mimic human decision-making to perform tasks, where the computer develops or is given a set of rules to follow that it then draws on to help it evaluate scenarios
- **machine learning** - a subset of AI where the computer "learns" and adapts based on new information
- **deep learning** - a subset of machine learning that uses multi-layered, artificial neural network algorithms that enable the computer to recognize patterns and classify data

![three nested circles, with artificial intelligence as the largest circle, inside of which there is machine learning, and inside of that there is deep learning and neural networks](https://github.com/YaleDHLab/lab-workshops/blob/master/neural-style-transfer/images/examples/ai-circles.jpg)

<br>AI receives a lot of attention for its use in industry (self-driving cars) and surveillance (face detection), but it's also providing new ways for interacting with and thinking about texts and images.

### Popular Approaches

#### Generative Adversarial Networks

["Is Artificial Intelligence Set to Become Art's Next Medium?"](https://www.christies.com/features/A-collaboration-between-two-artists-one-human-one-a-machine-9332-1.aspx) In October 2018, Christie's became the first auction house to sell art that was created with a generative adversarial network (GAN). GANs have two parts to them: a generator, which tries to create images that resemble its training set, and a discriminator, which tries to identify the fake, generated images from the real ones. 

#### Combinations of Machine Learning Algorithms

["The Next Rembrandt: Can the Great Master Be Brought Back to Create One More Painting?"](https://www.nextrembrandt.com/) In an effort to generate an image that would most closely resemble Rembrandt's subject matter and style, the Next Rembrandt project studied recurring features across 346 of his paintings. They used a range of techniques, from scanning the surface of his paintings to study their texture to programming a face detection algorithm to identify their common geometric patterns.

#### Image Animation
[First Order Motion Model for Image Animation](https://aliaksandrsiarohin.github.io/first-order-model-website/) This technique takes a source image and a video in order to animate the image, making it look as though it were a video clip.

#### Neural Style Transfer

Neural style transfer, which uses [convolutional neural networks](https://en.wikipedia.org/wiki/Convolutional_neural_network), takes the "style" of one digital image and applies it to the "content" of another, producing a new, generated output image as a result. One of the advantages of neural style transfer is that it does not require a large collection of images as other approaches (GANs) do in order to be successful. At a minimum, neural style transfer only requires you to supply two images.

Popular experiments highlighting this technique often take a very famous image with a marked style like Vincent Van Gogh's *Starry Night* to demonstrate what the algorithm is doing. In these cases, the final output image looks like a *Starry Night* filter has been applied to whatever the original content image was. But in practice, we can be more subtle or abstract. Depending on the software we're using, we will have access to parameters we can shift that tell the computer to keep or ignore the style image's color or to blur the content image before applying style to it, impacting the resulting output image. 

![three images that show Golden Gate Bridge, Starry Night, and a composite that shows the Golden Gate Bridge in the style of Starry Night](https://github.com/YaleDHLab/lab-workshops/blob/master/neural-style-transfer/images/examples/starry-night-example.jpg)

*above source images are from [Justin Johnson's GitHub Repository](https://github.com/jcjohnson/neural-style)* </br>

Questions we might ask with neural style transfer include but are by no means limited to:

* What can the approach tell us about what counts as "content" and "style" to humans? To computers? 
* What images work better as content or style images, and what does it mean that some work better than others? (We'd also have to define what we mean by "work better" — what is a successful neural style transfer outcome?)
* Can we use neural style transfer to create new forms? What about new art that combines the style of multiple artists or time periods?

## Set up your Workspace 

For this workshop, we'll experiment with two style transfer models using sample images I'll provide. But first, let's discuss how we'll set up our workspace.

### Folder & Filename Conventions

In order to keep track of our experiments (what images we used, what parameters we ran), let's establish a system for storing and naming our image files.

1. Create a new folder called "neural-style-experiments "on your Desktop (or somewhere you can access easily).

2. Inside that folder, create the following three folders:
* "content" - this will store the images we'll use as content images
* "style" - this will store the images we'll use as style images
* "output" - this will include the results of our experiments. 

3. Within "output," create the following folders:
* "adaptive-style-transfer"
* "adaIn-style-transfer"

Before we start running our experiments, we should also think about how we'll name our files. The convention I follow is:  
```
contentImageName-styleImageName-parameter1_parameter2.jpg
```
You may adopt this convention or devise one that feels more intuitive to you. Whatever you do, just do it consistently.

This folder & file structure will help us remember what we were working on, even if we return to the project months or years later.

*For extra insurance, we should also create a documentation.txt or readme.txt file that keeps track of each experiment we want to remember.*

### Images

The Google Drive folder at bit.ly/yale-dh-neural-style contains five content and five style images. Some of the images have more pronounced "content" or "style," and others are more subtle. We'll use only a few of the images in our activities below, but I encourage you to mix and match with the others as well. 

A quick note on the sample images: I added relatively small images (400 x 400 pixels) so that the output image will be generated quickly. You can use higher resolution images in RunwayML; it will just take the model more time to run (which in turn uses up more of the free credits Runway provides). Also, depending on your goal, you don't necessarily need high-resolution images in order for the model to be successful, so you might start out with a lower resolution image and work your way up as needed.

To get a sense for how the size of the content image impacts the resulting output image, I've included two output images below. The larger image had an input image of around 1000 pixels, while the smaller image had an input of around 500 pixels. Some detail is lost as a result of cutting the resolution of the content image in half, but depending on the level of fidelity or abstraction that you're going for, that might be ok.

![the Golden Gate Bridge in the style of Monet](https://github.com/YaleDHLab/lab-workshops/blob/master/neural-style-transfer/images/output/adaptive-style-transfer/goldenGateBridge-monet1000px.jpeg)

![the Golden Gate Bridge in the style of Monet with slightly fewer colors](https://github.com/YaleDHLab/lab-workshops/blob/master/neural-style-transfer/images/output/adaptive-style-transfer/goldenGateBridge-monet400px.jpeg)

## Generate Images with RunwayML

Designated "a machine learning tool for creators," RunwayML is a platform for applying machine learning to digital content that does not require any programming on the part of the user. You can also use it to train and publish your own models. At least while it is in beta, it is free to use up to a point (you get $10 in credits; it costs $0.05 per minute to run models and $0.005 per step in training models). 
 
To launch the application:
1. Download [RunwayML](https://runwayml.com/) by clicking on one of the green "Download Beta" buttons.
2. Once it downloads, double-click on the RunwayML icon.
3. The screen that loads will have the following prompts: "Browse Models," "Open Workspaces," "Train a Model." Click on "Browse Models."
* Models are the result of training an algorithm on a dataset — they represent the rules the algorithm has devised in order to perform a task
* From the "Browse Models" screen, you can find models that were trained on images, texts, or vectors in order to perform object detection, generate fake images, explore latent space of images, and apply style transfer.
* If you accidentally (or intentionally) click away from the Models screen and want to get back, click on the cube symbol on the left-hand side of the application
4. Click the dropdown by "Category" (toward the middle-top of the page) and select "Style Transfer" to see what models are available to us.
* At the time of this workshop, there are five models. The lower left-hand corner of each model shows that four of the models have been published with "Commercial Use" licenses, while one has a "Custom License" (more on licenses later).
* The lower right-hand corner reveals the popularity of each model within Runway, which could be used to indicate how well they're performing for people (the caveat, here, is that some of the models are newer than others, so a lower score isn't always an indication that a model is out of favor).

### Experiment 1: Adaptive Style Transfer, Limited Selection of Styles

We're going to start with the most popular model on Runway, "Adaptive Style Transfer." 

1. Let's start by taking a quick look at the model's documentation. To do that, find the model, hover over the lower left-hand corner, and click on "Learn More."  
* This will take us to a page with important information about the model that we may want to read before running anything: what is the model trained to do, are there licensing restrictions as to how the model can be used, is there a GitHub repository we could go to in order to see the code, has there been a publication using the code that we could read, and if the information is really good, it will also indicate what the training dataset was.
* Without getting in the weeds technically, we can see that this model was constructed with a conscious effort to add artists into the evaluation loop.
* Scrolling down shows us the authors behind the model. Scrolling further shows there's a paper and GitHub repository we could follow up with if we like the results or want more of the technical information.
* Back at the top of the page, click on "Gallery" for a preview of the results we can expect.
* Click on "License" to see the terms of use. With this model, it can be used commercially so long as attribution is given.
2. Now that we have more of a sense for this model, click the dropdown by the "Add To Workspace" blue button at the top right of the application, and select "New Workspace."
3. Give the workspace a name that will help you identify it later. I'll call mine: "DHLab-workshop."
4. Now that we're in the workspace screen, we can see the interface for the model we've loaded in the middle, and on the left-hand column, we'll see other workspaces we've created.
5. The Adaptive Style Transfer model contains a place for an "Input Type" (this will be where we upload a content image) and an "Output" (the results of applying the model to our input image). The style options exist on the right-hand column. Unlike the AdaIN model we'll experiment with next, this model limits our style inputs. We can currently select amongst thirteen artists. The innovation of Adaptive Style Transfer is that each artist represents its own model. The authors trained the algorithm on a collection of paintings from the specified artist, whereas some other popular models only train the algorithm on a single painting. The project team is also regularly adding new artists to the list, so if you like the results, this could be a model to keep an eye on. If we scroll below the style options, we can see what parameters we can control in order to adjust how the algorithm is working (the options don't always appear unless you specify a content image). More on parameters later.
6. Select the style you would like to try first. I'm going to select "Monet."
7. To add a content image, click the dropdown by "Input Type" and select "File" -> "Open Directory." Navigate to our project folder and select the "content" directory. This will load our content images into RunwayML so that we can move between them quickly.
8. Select "goldenGateBridge.jpg."
9. Click the purple "Run Remotely" button in the lower right-hand corner in order to run the model. You can tell it's working when it turns pinkish and says "Starting (Click to Stop)." It could take a minute or two to run.
10. When the button turns a solid pink and says "Stop," click on it to stop the model.
11. If you want to save the generated output image, click the small blue circle in the lower right-hand corner of the "Output" section. Don't forget to follow our naming convention: "goldenGateBridge-monet.jpg". Save the image to the "adaptive-style-transfer" folder in the "output" directory.
12. For a second image from this model we can use as a frame of reference for how well it's working, let's see how the model does with Van Gogh (you have to scroll all the way down the artist styles to find him). Apply this model to the Golden Gate Bridge as well, and save the output when it finishes. 

### Experiment 2: AdaIN Style Transfer, Custom Styles
1. Return to the "Browse Models" screen by clicking on the cube symbol on the left-hand column.
2. Click the dropdown by "Category" and select "Style Transfer."
3. This time, find "AdaIN-Style-Transfer" (short for adaptive instance normalization) and click on "Learn More." As the description highlights, the advantage of this model is that we'll be able to add our own style images, along with our own content images. We'll also have the option to adjust more of the parameters that inform how the model works. For more information on the specific implementation, you can click on the "GitHub Repository" link at the bottom, which will take you to the source code. As before, the "Gallery" tab provides a preview of what we can expect. The "License" tab indicates that this model can be used and modified for commercial purposes or private use, with the one condition being that you have to include the copyright statement.
4. Click the "Add to Workspace" blue button. In general, you can either add it to the workspace we've already created, or you can create a new one, but for this workshop, add it to the same workspace (we'll need our models together for one of the activities later on).
5. In order to compare this model with the last one, let's stick with the Golden Gate Bridge for now. Add it as our content image by clicking the "Input Type" dropdown and selecting "File" -> "Open File." (Loading only a single file at a time guarantees we'll have parameter options in the right-hand column.) 
6. Let's add out style image now. With AdaIn, we have the freedom to add our own style image, but keep in mind that we're limited to one style image at a time (the previous model was trained on multiple paintings by the same artist). So that we can have a more accurate comparison of the models, click "Input Type" -> "File" -> "Open File" and select Claude Monet's *Water Lilies*.
7. Click "Run Remotely." This model can take longer to run, especially with larger files. Let's talk through a few of the content and style parameters while it's working.
* Color determines whether you retain the content image's color (the default it to take color from the style image).
* Alpha affects how much of the style is pulled in, with a value of 1 leading to the strongest stylistic resemblance to the style image.
* Gaussian Blur blurs the content and/or style image before applying the model. This is helpful if you want a more abstract output.
8. What do you think of the output? 
9 Experiment on your own for a few minutes, changing the parameters on the right. One of my favorite tweaks was to adjust the Alpha to 0.79 and the Gaussian Blur for the content to 7.
10. Save any and all outputs that you like. Don't forget to follow the naming convention so that you can recreate them later! For example, here is the filename for the settings I liked above:
```
goldenGateBridge-waterLilies-alphap79_cgb7.png
```

### Experiment 3: Adaptive & AdaIN, Output as New Input
1. Staying within the AdaIn Style Transfer model, let's add a new content image. Click the dropdown and this time, let's select the output image from our Adaptive Style Transfer experiment.
2. For the style image, select Yayoi Kusama's *Resplendent Stars of the Universe*.
3. Save the output file — be sure to include some indication that we used the output from the Adaptive Style Transfer model:
```
ast_golden_monet-resplendent
```

## Run your own Experiments

Now that we've sampled a couple models for style transfer, return to the one that intrigued you the most and run more experiments with your own images or with some of the additional sample images in our content and style folders. You might also run some of the other models we haven't tried in order to see their strengths and limitations.

## Next Steps & Additional Tips
* Since Runway is currently in Beta, new models and workflow features are added and updated regularly, so log in occasionally to see what's new.
* For running neural style transfer without RunwayML, try [Justin Johnson's implementation](https://github.com/jcjohnson/neural-style). To get this code running on your own computer will require some experience with programming and setting up computer environments. It also has hardware constraints in that it performs better with a graphical processing unit (GPU). But, what it gives you is the ability to import multiple style images at the same time, declaring how much you want to take from each style image. It also includes more fine-tuned parameters that you can adjust. 
* Want to read up on neural networks and style transfer? Here are a few articles and papers that might be of interest:
  * [Runway's documentation](https://learn.runwayml.com/#/)
  * ["Art & AI: The Logic Behind Deep Learning ‘Style Transfer’"](https://medium.com/codait/art-ai-the-logic-behind-deep-learning-style-transfer-1f59f51441d1)
  * ["Neural Style Transfer: Creating Art with Deep Learning using tf.keras and eager execution"](https://medium.com/tensorflow/neural-style-transfer-creating-art-with-deep-learning-using-tf-keras-and-eager-execution-7d541ac31398)
  * ["Neural Artistic Style Transfer: A Comprehensive Look"](https://medium.com/artists-and-machine-intelligence/neural-artistic-style-transfer-a-comprehensive-look-f54d8649c199)
  * ["Artistic Style Transfer with Convolutional Neural Networks"](https://medium.com/data-science-group-iitr/artistic-style-transfer-with-convolutional-neural-network-7ce2476039fd)
  * ["Experiments with Neural Style Transfer"](https://genekogan.com/works/style-transfer/)
  * ["Neural Font Style Transfer"](https://ieeexplore.ieee.org/stamp/stamp.jsp?tp=&arnumber=8270274&tag=1)
* Want more technical training on neural networks? Here are a couple resources to check out:
  * [Free class on convolutional neural networks](https://www.coursera.org/learn/convolutional-neural-networks)
  * [YouTube video on convolutional neural networks](https://www.youtube.com/watch?v=FTr3n7uBIuE)
