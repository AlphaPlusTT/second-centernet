# second-centernet
development
```
second-center-v4
Car  AP@0.70, 0.70, 0.70:
bev  AP:96.09, 89.39, 86.67
3d   AP:92.04, 80.67, 77.50

second-center-v3
Car  AP@0.70, 0.70, 0.70:
bev  AP:96.00, 89.22, 86.64
3d   AP:91.23, 80.05, 77.02

second-center-v2
Car  AP@0.70, 0.70, 0.70:
bev  AP:94.45, 86.20, 83.57
3d   AP:89.54, 78.47, 74.10

second-center
Car  AP@0.70, 0.70, 0.70:
bev  AP:87.71, 82.86, 81.26
3d   AP:79.81, 71.51, 70.02

second-anchor
bev  AP:95.87, 89.63, 86.98
3d   AP:92.24, 83.11, 80.22
```
## TODO List
* 细节
  - [x] second的RPN最后是用的1x1卷积，而目前的centernet的3个head都是用的1x1卷积，是否考虑和centernet一样先过3x3卷积再过1x1卷积？这样的话RPN的最后一层是否需要调整？
  - [x] 计算高斯半径的方法（目前仍然使用的是cornernet的角点半径计算方法第一版，修改此项需要对focal_loss调参）
  - [x] 空的体素是否需要特殊处理
  - [x] 目前看来centernet在训练过程中，中心点的预测与尺度估计是分开的，但是在预测时这两者是假设一致的，所以在训练的时候把index的范围扩大（从中心扩大到中心及邻域）会提高回归的效果？
  - [x] eval_oracle_wh和eval_oracle_reg的作用？
  - [ ] offset的输出是否需要经过sigmoid，因为gt全为正，且在[0, 1]之间，更进一步的来讲，确定中心点在特征层上的位置时，应该用round而不是floor
  - [x] 中心点溢出的问题目前是设置阈值，是否采取删除操作更合适？
  - [x] 高度值的预测是否需要encode和decode的操作？
  - [x] centernet使用像素尺寸计算输出特征图上对应的高斯半径？目前的网络是用的特征图的目标尺寸计算的高斯半径
  - [x] 目前除了heat_map_head之外，没有经过decode和encode．
  - [x] centernet中对于size的回归写了三种loss，目前采用的是跟offset一样的L1 loss．
  - [x] centernet训练和测试的时候使用的是不同的sigmoid？
* 问题
  - [x] kitti.py中生成bbox和heat map的gt的流程是一样的，但是生成的tensor变量分别是list类型和tensor类型
  - [x] numpy的clip不能用于多线程?

