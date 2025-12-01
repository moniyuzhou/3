# VASP计算类型流程图

## 流程图
```mermaid
flowchart TD
    A[VASP计算类型总览] --> B[按离子运动分类]
    A --> C[按电子迭代分类]
    A --> D[实用提示]

    B --> B1["静态计算<br>NSW=0<br>'单点计算'"]
    B --> B2["离子运动计算<br>NSW>0<br>'多点/巡游计算'"]
    
    B1 --> B1a["自洽场计算 (SCF)<br>目的:获取总能/电荷密度<br>INCAR: NSW=0, ICHARG=2(可选)"]
    B1 --> B1b["非自洽计算 (NSCF)<br>目的:获取能带/DOS<br>INCAR: NSW=0, ICHARG=11"]
    
    B2 --> B2a["结构弛豫/优化 (Relaxation)<br>IBRION=1(准牛顿), 2(CG), 3(DMD)"]
    B2 --> B2b["分子动力学 (MD)<br>IBRION=0, SMASS<3"]
    B2 --> B2c["过渡态搜索 (TS)<br>IBRION=3, 5(CI-NEB)"]
    B2 --> B2d["声子/振动频率计算<br>IBRION=5,6,8"]

    C --> C1["自洽迭代 (SCF)<br>密度与势场循环直至收敛<br>NELM=最大步数"]
    C --> C2["非自洽 (NSCF)<br>固定势场单步求解"]
    C --> C3["含时/微扰理论<br>如GW/BSE/DFPT"]
    
    D --> D1["💡 SCF→NSCF常见流程"]
    D --> D2["💡 Relaxation需要逐步收紧EDIFFG"]
    D --> D3["💡 不同IBRION对应不同算法"]
    
    %% 添加一些连接关系
    B1a -.->|"提供电荷密度"| B1b
    B2a -.->|"收敛结构用于"| B1
    C1 -.->|"电子收敛后"| B1a
