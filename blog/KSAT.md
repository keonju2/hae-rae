# Ko-KSAT benchmarks for LLM models

### Introduction

The Ko-KSAT dataset team aims to evaluate the language model's Korean language proficiency by creating a dataset of the Korean SAT(대학수학능력평가, 수능), similar to the English SAT and LSAT datasets.  
All data from the Korean SAT are provided in pdf format, and are made in multi-stage form. So we created a dataset that was converted to Text form by copying and pasting directly.   

### Dataset

We collected data from the KSAT (수능) administered from 2007 to 2022.   
  
| Currirulum     | Year        |Size        |
| :------------- | :---------- |:----------|
| 7th curriculum | 2007 - 2011 |45        |
| 2007 revised   | 2012 - 2016 |Year        |
| 2009 revised   | 2017 - 2020 |Year        |
| 2015 revised   | 2021 - 2023 |Year        |

### Details

For KSAT, expressions referring to a part of the text are used, and problems interpreting tables and graphs appear.  
The dataset has undergone several processing steps to ensure that the language model can understand them.

1. Tokens have been added to areas that refer to sentences, paragraphs, images, and tables referred to in the problem.

| Token                    | Meaning               | Example       |
| :----------------------- | :-------------------- | :------------ |
| < part start >, < part end > | paragraphs            | (a), (b), (c) |
| < par start >, < par end >   | word,sentence         | (ㄱ), (ㄴ), (ㄷ) |
| < etc start >, < etc end > | image, tables, graphs | Latex, Text   |


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
ㄱ. 여성 취업자 중 전문 관리직 종사자 구성비율 {[}단위: 백분율{]} & 11.4  & 14.0  & 17.5  \\ \hline
ㄴ. 가입 여성 1인당 출산율 {[}단위: 명{]}              & 1.65  & 1.47  & 1.08  \\ \hline
ㄷ. 전체 인구 중 30대 미혼 인구 비율 {[}단위: 명{]}       & 1.71  & 2.40  & 3.75  \\ \hline
ㄹ. 평균 수명 {[}단위: 세{]}                      & 72.3  & 74.6  & 76.8  \\ \hline
\end{tabular}
\end{table}
<etc end>
```
### Benchmark Method
For Bard, GPT-turbo 3.5, and HyperClova LK-D2, the prompts used are as follows.
```
다음 질문을 읽고 아래 선택지 중 가장 적절한 답의 번호를 고르시오.
### 문제: {문제 내용}
### 참고: {문학 작품 등 보기 내용}
### 선택지: {1~5번의 선택지 내용}
### 정답:
```
The evaluation method for Polyglot-Ko, KoAlpaca, Kullm, XGLM, KoGPT, and mT5 is likelihood.   
After evaluating the probability of question-answer pairs for each option, the option with the highest log likelihood is presented as the answer.   
The evaluation may differ from the generator method.  
Problems with token length exceeding 2048 are excluded.  


### Result
Generator Evaluation
| Model | Accuracy |
| --- | --- |
| GPT-turbo 3.5 | 0.31 |
| Bard | 0.36 |
| HyperClova LK-D2 | 0.18 |

Log Likelihood Evaluation
| Model | Accuracy |
| --- | --- |
| polyglot-ko-12.8b | 0.18 |
| KoAlpaca-Polyglot-12.8B | 0.14 |
| kullm-polyglot-12.8b-v2 | 0.18 |
| kogpt6B-ryan1.5b | 0.21 |
| xglm-7.5B | 0.21 |
| mt5-xl | 0.20 |


### Contributors 
나건주  
박수빈  
박은우  
손규진  
염제원  
유수빈  
조하늘  
진혜원  
### Copyright
The copyright of this material belongs to the Korea Institute for Curriculum and Evaluation(한국교육과정평가원) and is prohibited from using it for research purposes.
