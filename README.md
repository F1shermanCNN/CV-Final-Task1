### 2DGS(Object A and Background Scene)
## 环境配置
#首先创建环境，要求python=3.10,cuda=11.8

#安装colmap

#安装依赖
```bash
pip install -r requirements_2dgs.txt
```

#下载Kobe数据集,放在本地的data文件夹下:

https://drive.google.com/drive/folders/104ITdruMWy3bJy7J_qOayYOE7LNySR8B?usp=sharing

(或者下载Mip-NeRF 360 数据集中的 garden)

#提取位姿:
```bash
python convert.py -s data
```
#开始训练:
```bash
python train.py -s data -m data/output
```

### Threestudio(Object B and C)
#首先创建环境，要求python=3.10,cuda=11.8

#安装依赖
```bash
pip install -r requirements_threestudio.txt
```

#Object B训练示例:
```bash
python launch.py --config configs/dreamfusion-if.yaml --train --gpu 0 system.prompt_processor.prompt="a zoomed out DSLR photo of a baby bunny sitting on top of a stack of pancakes"
```

#Object C数据下载

https://drive.google.com/drive/folders/104ITdruMWy3bJy7J_qOayYOE7LNySR8B?usp=sharing

#Object C训练示例:
```bash
#coarse
python launch.py --config configs/magic123-coarse-sd.yaml --train --gpu 0 data.image_path=load/images/hamburger_rgba.png system.prompt_processor.prompt="a delicious hamburger"
#refine
python launch.py --config configs/magic123-refine-sd.yaml --train --gpu 0 data.image_path=load/images/hamburger_rgba.png system.prompt_processor.prompt="a delicious hamburger" system.geometry_convert_from=path/to/coarse/stage/trial/dir/ckpts/last.ckpt
```
