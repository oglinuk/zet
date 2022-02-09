# Nvidia is no Longer Acquiring ARM

"SANTA CLARA, Calif., and TOKYO – Feb. 7, 2022 – NVIDIA and SoftBank
Group Corp. (“SBG” or “SoftBank”) today announced the termination of the
previously announced transaction whereby NVIDIA would acquire Arm Limited
(“Arm”) from SBG. The parties agreed to terminate the Agreement because
of significant regulatory challenges preventing the consummation of the
transaction, despite good faith efforts by the parties. Arm will now
start preparations for a public offering."

To understand why this is so big, let's do a thought experiment. Think
about the process training process of an AI. The reason AI has had such a
boom since 2012, is due to the introduction of training deep neural
networks on Graphical Processing Units (GPUs). This drastically reduced
the time it took to train an AI model. To understand why GPUs accelerated
AI, it is best explained by a CPU vs GPU mythbusters video referenced
below. When training, currently the *only* commercially viable option is
using Nvidia's compute stack: CUDA and cuDNN. There is an open
alternative being developed called SYCL (referenced below), but unsure of
it's use at this time.

In 2014, Nvidia brought out the Jetson TK1 DevKit. We will come to
understand why this is important later, but for now the only thing to
understand is it is a small/powerful ARM-based Linux computer.

Google then introduced a Tensor Processing Unit (TPU) in 2016, which is
hardware designed specifically for machine learning (and tensorflow their
AI framework). In 2020 Nvidia then announced it's own version of a TPU,
called a Tensor Core.

The AI industry is shifting to something called *edge-computing*, which
is outside the scope of this zet, but have referenced below. Essentially
it is just shifting the AI from running in a cloud provider, to running
it on a small device out in world. The Nvidia Jetson is one such device.

Not only is ARM used for Nvidia's Jetson range, but it is also what most
(if not all) mobile phones and smaller devices use (will leave that as a
challenge for you to go spelunking on your own).

Related:

* Nvidia and SoftBank Group Announce Termination of NVIDIA’s Acquisition of Arm Limited
	<https://nvidianews.nvidia.com/news/nvidia-and-softbank-group-announce-termination-of-nvidias-acquisition-of-arm-limited>
* CPU vs GPU Mona Lisa
	<https://www.youtube.com/watch?v=0udMBdo0Rac>
* CUDA
	<https://developer.nvidia.com/cuda-zone>
* cuDNN
	<https://developer.nvidia.com/cudnn>
* SYCL
	<https://www.khronos.org/sycl/>
* Jetson TK1 DevKit
	<https://www.phoronix.com/scan.php?page=news_item&px=MTY0MzE>
* Google Tensor Processing Unit (TPU)
	<https://cloud.google.com/blog/products/ai-machine-learning/google-supercharges-machine-learning-tasks-with-custom-chip>
* Nvidia Tensor Core
	<https://www.nvidia.com/en-us/geforce/news/nvidia-dlss-2-0-a-big-leap-in-ai-rendering/>
* Edge Computing
	<https://www.nvidia.com/en-us/data-center/edge-computing/>

Tags:

	#arm #nvidia #jetson #edge-computing #ai #cuda #cudnn #gpu #tpu
