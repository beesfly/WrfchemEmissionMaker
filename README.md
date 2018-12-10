# WrfchemEmissionMaker
基本上是一个读取wrfchem的初始条件（即real.exe生成的wrfinput文件）的网格设置，然后生成对应的wrfchem所需排放源文件的脚本。

生成的排放源格式：io_style_emissions= 1,emiss_inpt_opt=101。（相关含义不清楚的请参阅wrfchem的user guide)

注意！！！由于清华meic源的区域只包括中国大陆（区别于mix的整个东亚），因此wrfchem的网格区域最好设置在中国大陆及周边沿海地区。

===============分割线===============

准备工作：

保证计算机中已安装：

1. ncl，版本6.3及以上。包扩ncl中自带程序WRAPIT，该程序可使ncl脚本调用一个fortran函数。

2. python3。推荐安装最新版本anaconda3。

3. gfortran/gcc/g++。

如何使用

1.创建脚本工作目录。

2.将wrfchem_emission_maker.py放入该目录。

3.在工作目录下新建名为emidata、wrfinput、wrfchemi的三个目录

4.将从 http://www.meicmodel.org 下载的原始格式分月的meic排放源文件放入emidata文件夹。需要保证emidata下的文件夹命名为{YYYYMM}，如./201602.该月所有nc、asc和xml文件均直接位于{YYYYMM}文件夹下。

5.修改wrfchem_emission_maker.py文件中main函数内如下变量：
例：base_year="2016"   #清华源原始数据年份
    base_month="8"     #清华源原始数据月份
    program_dir="/home/IncubatorShokuhou/wrfchem_emission_maker" #python程序所在目录
    wrfinput_path="/home/IncubatorShokuhou/wrfchem_emission_maker/wrfinput" #wrfinput文件所在目录
    wrfchemi_out_path="/home/IncubatorShokuhou/wrfchem_emission_maker/wrfchemi" #排放源文件输出目录

6.将执行real.exe后生成的wrfinput_d*文件移动至上一行确定的wrfinput_path目录，并添加.nc的后缀。

7.运行wrfchem_emission_maker.py。

完成！排放源文件生成在上述wrfchemi_out_path目录。