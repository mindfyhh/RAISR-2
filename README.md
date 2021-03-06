实现论文：Y. Romano, J. Isidoro, and P. Milanfar, "RAISR: Rapid and Accurate Image Super Resolution"

环境：Matlab R2016a

直接运行` runRAISRTest.m` 就能完成训练和测试的全过程。可以直接更改 scale 和 LR_patch_size 的值，训练代码能根据给定的这两个参数来进行新的训练。

RAISR 的训练过程较长，因为要从插值后的 HR 图像中提取 patch，大概需要 3-4 小时。训练好的结果已经保存在 `RAISR_result` 文件夹下，直接把 `runRAISRTest.m` 的 22、23 行注释掉就能直接进行测试。

## 结果

用的 patch_size 为 11，scale 为 3，从训练图像中提取出了 7000w 的 patch 进行训练。

计算时间在 MacOS, 2 GHz Intel Core i5,  8 GB 1867 MHz LPDDR3 下进行测试得出；**其中用的 Bicubic 方法为自己实现的，没有实现 Antialiasing 功能**：

|     Set14      | Bicubic  |          |   RAISR   |          |            |
| :------------: | :------: | :------: | :-------: | :------: | :--------: |
|                | **PSNR** | **SSIM** | **PSNR**  | **SSIM** |  **Time**  |
|   **baboon**   |  21.53   |   0.54   | **23.39** | **0.60** | **28.01s** |
|  **barbara**   |  24.74   |   0.76   | **26.48** | **0.78** | **49.26s** |
|   **bridge**   |  23.42   |   0.66   | **24.85** | **0.70** | **31.38s** |
| **coastguard** |  25.20   |   0.63   | **26.97** | **0.66** | **12.16s** |
|   **comic**    |  22.55   |   0.72   | **24.09** | **0.76** | **10.05s** |
|    **face**    |  31.66   |   0.78   | **33.61** | **0.82** | **8.62s**  |
|  **flowers**   |  26.88   |   0.81   | **28.43** | **0.84** | **21.98s** |
|  **foreman**   |  28.69   |   0.90   | **31.24** | **0.92** | **12.25s** |
|   **lenna**    |  31.40   |   0.86   | **33.15** | **0.88** | **29.24s** |
|    **man**     |  26.28   |   0.75   | **27.88** | **0.79** | **32.24s** |
|  **monarch**   |  29.17   |   0.92   | **30.96** | **0.93** | **50.26s** |
|   **pepper**   |  29.47   |   0.86   | **31.65** | **0.88** | **31.51s** |
|    **ppt3**    |  23.29   |   0.89   | **24.82** | **0.91** | **42.16s** |
|   **zebra**    |  26.69   |   0.81   | **28.65** | **0.84** | **27.63s** |
| ***AVERAGE***  |  26.50   |   0.78   | **28.30** | **0.81** | **28.13s** |

结果也与论文给出的测试结果相近：

![a4](https://i.loli.net/2018/01/23/5a6611891a104.jpg)

选部分结果进行展示：

![r7](https://i.loli.net/2018/01/23/5a66119f3c618.jpg)

baboon 的鼻子处的噪点更平滑了。

![r6](https://i.loli.net/2018/01/23/5a6611aaabe46.jpg)

flowers 的所有过渡的边缘部分都变得没有那么锐利，过渡更自然。

![r5](https://i.loli.net/2018/01/23/5a6611b3cd2c9.jpg)

foreman 的结果有了很大的提高，主要是因为后方墙壁的边缘很好的平滑掉了，SF 的结果中墙壁的边缘有很多噪点，而 RAISR 的中不会出现。

![r4](https://i.loli.net/2018/01/23/5a6611bfdfe0b.jpg)

![r3](https://i.loli.net/2018/01/23/5a6611cc1a49d.jpg)

可见 RAISR 的结果比 SF 看起来都更加自然和平滑，并且基本都有更高的 PSNR 值。