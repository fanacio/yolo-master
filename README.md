## 说明
###    对于数据集的准备

    第一种方式：
    数据格式如下所示
    |-- images
    |-- labels
    |-- spicy
    |-- spicy.data
    |-- spicy.names
    |-- train.txt
    |-- val.txt
    |-- yolov3_spicy.cfg

    images下和labels下的目录结构为：

    |-- train2014
    `-- val2014

    存放了图片和标注好的结果txt（一一对应）
    参考以下链接：
    https://blog.csdn.net/qq_38316300/article/details/106771964

## 关于cfg文件的写法

    训练时候：
    打开 yolov3-obj.cfg 将 第三行第四行注释掉 将第六行和第七行注释取消
    将batch设为batch=64，将subdivisions设为subdivision=8;

    如果显存较小（训练时候报错了out of memory）则将batch调小（32，16，8等），但是要保证batch是subdivisions的整数倍。同时取消多尺度训练：即设置random=0（这个参数在yolo层）；

    关于max_batches的设置，其应该设置为 检测的目标个数*2000；

    关于steps的设置，其应该设置为max_batches *0.8, *0.9;

    关于classes(yolo层)，几类改成几类即可；

    关于filters的修改（yolo层的上一个卷积层），其等于（classes+5）*3;

    总之，训练前除了数据集还需要准备以下文件：
        >>1.根据README.md文件下载正确的预训练权重；
        >>2.obj.data
        >>3.obj.names
        >>4.yolov*_obj.cfg
        >>5.train.txt和val.txt