# The World of GPU's

Here at Runway, you may sometimes see an icon asking you if you'd like to use a GPU. But what exactly is a GPU, why should you care, and why do you even need one?

## What is a GPU?

GPU stands for Graphics Processing Unit. It's most often used in computers, to display images to monitors. Previously GPU's were used for rendering games, but now they are more often being used in AI advancements.

You may have also heard of the term CPU (central processing unit). A CPU is present in all computers and is often referred to as the brains of a computer. GPU's are different from CPU's, as a GPU can only do a fraction of the amount of work that a CPU can, but with at an incredibly high speed. As a result GPU's are very powerful and are now being used in ways beyond rendering images.

## GPU's and AI

In recent years, GPU's have been part of the driving force behind why we see so much advancement within AI. GPU's have allowed us to learn faster from vast amounts of data.

Many of our computers running Mac, Windows or Linux, may have a GPU under-the-hood. Currently Nvidia is the main provider of GPU's for AI and what we call deep learning. Then we have Google who formed a chip called the TPU also for AI. How ever not all GPU's are not yet ready for AI.

## Has my Machine got a GPU?

Here we have a guide depending on your OS, of how to identify if you have a GPU.

<!-- tabs:start -->

#### **Windows**

1. Click Start
2. On the Start menu, click Run
3. In the Open box, type "dxdiag" (without the quotation marks), and then click OK
4. The DirectX Diagnostic Tool opens. Click the Display tab
5. On the Display tab, information about your graphics card is shown in the Device section. You can see the name of your card, as well as how much video memory it has.

!> Newer Windows often do have a GPU in them! Currently our models support NVidia GPU's.

#### **Mac**

Some MacBook Pro's have one of the following GPU's:

* AMD Radeon Pro Vega 16
* Vega 20,
* Radeon Pro 555X
* 560X GPUs

In order to check if your Mac has a GPU.

1. Apple () menu > About this Mac
2. Overview > System Report
3. Hardware > Graphics/Displays
4. Look at the 'Type' field on this panel. If it says GPU, then you do have a GPU

!> Note that although newer versions of Macs do have a GPU, some models will not work with this GPU type. This is because many AI models, use NVidia GPU's. There are wider community groups working on forming models that will work on a  wider GPU basis.

#### **Linux**

Coming soon!
<!-- tabs:end -->

## GPU's in the Cloud

Some of the models you may wish to run remotely (on the 'cloud') as opposed to locally, for example, to use a GPU for a model. Luckily we added the ability to do this!

In order to run remotely, use the toggle switch within your workspace. This allows you to choose if you want to run on your machine or run in the cloud. Here we see the toggle allows us to 'Enable Remote GPU'

![Remote GPU](images/model_101/running_remotely.png)