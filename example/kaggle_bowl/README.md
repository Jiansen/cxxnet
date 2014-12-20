
* Resize all image to 48 X 48 * 

跳过下面
```
mkdir /home/cxxnet/example/kaggle_bowl/data
python gen_train.py /home/data/bowl/train/ /home/cxxnet/example/kaggle_bowl/data/train/
python gen_test.py /home/data/bowl/test/ /home/cxxnet/example/kaggle_bowl/data/test/
```

直接下载 scale48x48.zip

sen把他解压到了
```
/home/ubuntu/data/
&
/home/cxxnet/example/kaggle_bowl/data/
```
ubuntu是ec2上的用户名，
```
/home/ubuntu/cxxnet/example/kaggle_bowl
```
是运行这些命令的位置

* Generate img list

Bing
```
python gen_img_list.py train /home/data/bowl/sampleSubmission.csv data/train/ train.lst
python gen_img_list.py test /home/data/bowl/sampleSubmission.csv data/test/ test.lst
```

sen
```
python gen_img_list.py train /home/ubuntu/data/sampleSubmission.csv /home/ubuntu/data/train/ train.lst
python gen_img_list.py test /home/ubuntu/data/sampleSubmission.csv /home/ubuntu/data/test/ test.lst
```


* Generate binary image file
First build im2bin at ```../../tools```, then run
```
../../tools/im2bin train.lst ./ train.bin
../../tools/im2bin test.lst ./ test.bin
```




* Run CXXNET
```
mkdir models
../../bin/cxxnet bowl.conf
```
It take about 5 minute to train a deep conv net model on Geforece 780

* Run Prediction
```
../../bin/cxxnet pred.conf
```
It will write softmax result in test.txt

* Make a submission file

```
python make_submission.py /home/data/bowl/sampleSubmission.csv test.lst test.txt out.csv
```

* Submit out.csv, you will get a result of 1.382285
