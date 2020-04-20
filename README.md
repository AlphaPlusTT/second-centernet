# second-centernet
development
```
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
  - [ ] ???
  - [ ] second的RPN最后是用的1x1卷积，而目前的centernet的3个head都是用的1x1卷积，是否考虑和centernet一样先过3x3卷积再过1x1卷积？这样的话RPN的最后一层是否需要调整？
  - [ ] 计算高斯半径的方法（目前仍然使用的是cornernet的角点半径计算方法第一版，修改此项需要对focal_loss调参）
  - [ ] 空的体素是否需要特殊处理
  - [ ] 目前看来centernet在训练过程中，中心点的预测与尺度估计是分开的，但是在预测时这两者是假设一致的，所以在训练的时候把index的范围扩大（从中心扩大到中心及邻域）会提高回归的效果？
  - [ ] eval_oracle_wh和eval_oracle_reg的作用？
  - [ ] offset的输出是否需要经过sigmoid，因为gt全为正，且在[0, 1]之间
  - [ ] 中心点溢出的问题目前是设置阈值，是否采取删除操作更合适？
  - [ ] 高度值的预测是否需要encode和decode的操作？
  - [ ] centernet使用像素尺寸计算输出特征图上对应的高斯半径？目前的网络是用的特征图的目标尺寸计算的高斯半径
  - [ ] 目前除了heat_map_head之外，没有经过decode和encode．
  - [ ] centernet中对于size的回归写了三种loss，目前采用的是跟offset一样的L1 loss．
  - [ ] centernet训练和测试的时候使用的是不同的sigmoid？
* 问题
  - [ ] kitti.py中生成bbox和heat map的gt的流程是一样的，但是生成的tensor变量分别是list类型和tensor类型
  - [ ] numpy的clip不能用于多线程?

