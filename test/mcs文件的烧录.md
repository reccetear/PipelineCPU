##MCS文件烧录##

>部分Nexy4参数：Nexy4板子的Serial(SPI) Flash容量为128 Mbit(或者说16 Mbyte，烧录进去的代码不能大于这个值)，为非易失性介质，也就是说掉电后代码依旧存储在里面，除非使用软件擦除掉，总线为x4(quad-mode)模式。

**生成MCS文件**

将要烧录到Serial Flash中的代码拷贝到utils/gen_coe/ram\_init\_gen/目录下，清除掉多余的.c与.S文件，执行make flash命令。（注意：依赖的ruby需要提前安装，另外如果提示vivado命令不存在，则要么在PATH中添加，要么直接在Vivado软件tcl中cd到该目录下，执行write\_cfgmem -force -format mcs -interface spix4 -size 16 -loaddata "up 0x0 rom.bin" -file main.mcs）

这样可以生成main.mcs文件，该文件则是最后需要烧录到Serial Flash中的文件。

**烧录MCS文件**

1、在Hardware Manager中，右键器件，选择Add Configuration Memory Device。

![https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step1.png](https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step1.png)

2、选择芯片Serial Flash参数，按*Manufacturer: Spansion, Type: spi, Density(Mb):128, width: x1_x2_x4*进行选择。

![https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step2.png](https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step2.png)

3、选择烧录的MCS文件。

![https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step3.png](https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step3.png)

4、出现以下情况则烧录成功。

![https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step4.png](https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step4.png)

![https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step5.png](https://github.com/NJUCS-ComputerSystemLab-2017/PipelineCPU/blob/master/ref/pic/mcs_step5.png)



**驱动Serial Flash**

我们使用了上一届提供的驱动代码，该代码是学校联系了Xilinx公司，由其工程师进行设计并写出的，其功能较为灵活，直接拿来使用即可符合我们的需求。