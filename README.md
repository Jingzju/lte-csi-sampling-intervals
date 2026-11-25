# 不同 CSI 采样间隔下的 LTE CSI 实测数据集

数据集编号 `2023YFB2904804-005`。本数据集记录了 2026 年 9 月 29 日在室内使用两台 USRP 2974 采集的 LTE 信道状态信息（CSI）。12 次连续采集共得到 11,518,556 条子载波观测，覆盖固定位置和移动条件。

## 下载

[下载 v1.0.0 数据包](https://github.com/Jingzju/lte-csi-sampling-intervals/releases/download/v1.0.0/lte-csi-sampling-intervals-v1.0.0.zip)（87,451,614 字节）。解压后得到以下四个目录。

| 采样间隔 | 目录 | CSV 文件数 |
| --- | --- | ---: |
| 20 ms | `test_20ms/` | 3 |
| 30 ms | `test_30ms/` | 4 |
| 40 ms | `test_40ms/` | 3 |
| 50 ms | `test_50ms/` | 2 |

压缩包 SHA-256 校验值为 `505ca160e5c189d170d2103c3d8d7249cb301bf1891d8d33efeb9b8fff8331ab`。

## 读取数据

每个 CSV 是一次连续采集，文件名记录采集开始时间。各行均为数据，无表头，五列依次为子载波号、CSI 实部、CSI 虚部、组号和时间戳。一个完整快照包含编号 1 至 200 的子载波。部分组记录不全，组号在每个文件内独立使用。

以下示例在解压目录中运行，使用 pandas 读取一个 20 ms 文件的前五行，并计算复数信道响应。

```python
from pathlib import Path
import pandas as pd

path = next(Path("test_20ms").glob("*.csv"))
columns = ["subcarrier", "real", "imag", "group", "timestamp"]
sample = pd.read_csv(path, header=None, names=columns, nrows=5)
sample["csi"] = sample["real"] + 1j * sample["imag"]
print(sample)
```

## 数据许可

本数据集采用知识共享署名－非商业性使用 4.0 国际许可协议（CC BY-NC 4.0）。你可以为非商业目的使用、修改和分享数据。分享原始数据或修改版时，请署名 **浙江大学ILAC课题组** 并注明数据来源，附上许可链接，并说明所做的修改。商业用途请另行取得授权。[许可说明](https://creativecommons.org/licenses/by-nc/4.0/deed.zh-hans) · [许可全文](LICENSE)

推荐署名：浙江大学ILAC课题组，《不同 CSI 采样间隔下的 LTE CSI 实测数据集》，v1.0.0，2026。[数据来源](https://github.com/Jingzju/lte-csi-sampling-intervals) · [CC BY-NC 4.0](https://creativecommons.org/licenses/by-nc/4.0/)
