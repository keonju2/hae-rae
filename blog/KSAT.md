# Ko-KSAT benchmarks for LLM models

### Introduction

The Ko-KSAT dataset team aims to evaluate the language model's Korean language proficiency by creating a dataset of the Korean SAT(대학수학능력평가, 수능), similar to the English SAT and LSAT datasets.  
All data from the Korean SAT are provided in pdf format, and are made in multi-stage form. So we created a dataset that was converted to Text form by copying and pasting directly.   

### Dataset

We collected data from the KSAT (수능) administered from 2007 to 2022.   
  
| Currirulum     | Year        |
| :------------- | :---------- |
| 7th curriculum | 2007 - 2011 |
| 2007 revised   | 2012 - 2016 |
| 2009 revised   | 2017 - 2020 |
| 2015 revised   | 2021 - 2023 |

### Details

For KSAT, expressions referring to a part of the text are used, and problems interpreting tables and graphs appear.  
The dataset has undergone several processing steps to ensure that the language model can understand them.

1. Tokens have been added to areas that refer to sentences, paragraphs, images, and tables referred to in the problem.

| Token                    | Meaning               | Example       |
| :----------------------- | :-------------------- | :------------ |
| < part start $>$, $<$ part end > | paragraphs            | (a), (b), (c) |
| < par start $>$, $<$ par end >   | word,sentence         | (ㄱ), (ㄴ), (ㄷ) |
| < etc start $>$, $<$ etc  end $>$ | image, tables, graphs | Latex, Text   |


2. Middle Korean(중세 국어) cannot be encoded, so it is excluded.  
3. Problems related to tables, graphs, and figures are changed to LaTeX syntax or texts containing only objective facts.
   For example, the expression in the example below is changed as follows:  

![image](https://github.com/keonju2/fingen/assets/54880474/d727dbab-884e-4234-bc98-9e0dd5ced4e0)

```
다음은 사회 변화에 대비한 복지 정책 에 관한 글을 쓰기 위해 수집한 자료를 정리한 내용이다 자료를 결합하여 해석하고 주제를 생성하는 과정으로 가장 적절한 것은?
<etc start>
\begin{table}[]
\begin{tabular}{|l|l|l|l|}
\hline
항목                                        & 1995년 & 2000년 & 2005년 \\ \hline
ㄱ. 여성 취업자 원) and is prohibited from using it for research purposes.
