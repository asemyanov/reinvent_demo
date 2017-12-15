# reinvent_demo

### Alexnet warmup

Step 1: Use AWS EC2 instances, 

First, Choose AWS Marketplace and search for Deep Learning. My favorite is AWS Deep Learning AMI (Ubuntu).
Then Choose p2.xlarge instance type (server type).  It features one node of Tesla K80 GPU. I recommend to use Tesla for testing different things and use Volta when you really know what you are doing since it's more expensive and faster.
Also I recommend to use CPU instances c5.large instances for low-scale dataset preparation, again because reasonable cost cutting is always good.
It's very easy to change instance types on the fly with AWS. You just have to stop your instance, then go to actions -> instance settings -> change instance type. After it you have to start it and that's all, 5 minutes for it

If you don't have limit available for p2.xlarge then go to page "Limits", it's on the top left corner, and click "Request limit increase", then make a letter with some information of what you gonna do with this type of instance. 

Second, choose some place on the disk. I usually use 50GB SSD plus additional 2TB cold HDD volume
For the instructions on how to attach additional AWS Volumes please go to 
http://docs.aws.amazon.com/AWSEC2/latest/UserGuide/ebs-using-volumes.html

Third, let's configure the security group
Click Add rule, put Port Range to 8888, and make sure Source set to Anywhere
Warning this is not super 100% safe solution in terms of web security, however it makes things much easier after it

Optional:
It would be really useful to assign AWS elastic ip to your instance in order to make sure that ip address


Step 2: Connect to your instance and clone this repository

`git clone https://github.com/asemyanov/reinvent_demo.git`




Step 3:
Activate preinstalled python environment with mxnet

`source activate mxnet_p36`

Then use find what ip is used for internet

`ifconfig`

Copy inet addr:

Then make a good and complicated password for your Juputer Notebook

`Juputer Notebook password`

Then launch jupter notebook. I prefer to use tmux for it

`tmux`

`juputer notebook --ip=#here is your ip address that you copied a while ago`

exit tmux with CTRL+b  d

If you want to get back to the jupyter process hit:
tmux ls
tmux a -t 0

Cool!

If you did it, you should be able to go to your web browser, type ip address of your intsance (take it from the AWS dashboard)
and add port 8888. 
It should look smth like:

132.143.122.19:8888



Step 4: open Alexnet-warmup-2 notebook and go through the cells


### Fine-tuning demo

step 0: quick review the previous information if you skipped it

step 1: download Food-101 dataset:

`wget http://data.vision.ee.ethz.ch/cvl/food-101.tar.gz`

step 2: unpack the archive with dataset

`tar xvzv ./food-101.tar.gz`

step 3: make .rec files out of dataset. it increases the speed of training. make sure to check path to /food-101/

`python im2rec.py --list True --recursive True --train-ratio=0.95 mydata ./food-101/images `

`python im2rec.py --resize 480 --quality 95 --num-thread 16 mydata ./food-101/images `

step 4: open finetuning1 notebook and go through the cells





Also I highly recommend this tutorial 
https://github.com/zackchase/mxnet-the-straight-dope
I think it's currently the best right now for Gluon and MXnet

