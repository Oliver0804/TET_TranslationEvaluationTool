# 翻譯評估工具

本專案提供了一個簡單的工具來計算翻譯結果的 BLEU 和 ROUGE 分數，以評估翻譯質量。

## 依賴項目

請確保已安裝以下 Python 套件：

- `numpy`

## 使用方法

### 計算 BLEU 分數

BLEU 分數用於衡量翻譯結果與參考語料庫的相似度，分數越高表示翻譯質量越好。

```python
from bleu import compute_bleu

# 準備參考語料庫和翻譯語料庫
reference_corpus = [
    [['this', 'is', 'a', 'test'], ['this', 'is', 'test']],
    [['another', 'test']],
    [['yet', 'another', 'example']],
    [['more', 'sentences', 'for', 'testing']],
    [['final', 'example', 'sentence']]
]
translation_corpus = [
    ['this', 'is', 'a', 'test'],
    ['another', 'test'],
    ['yet', 'another', 'example'],
    ['more', 'sentences', 'for', 'testing'],
    ['final', 'example', 'sentence']
]

# 計算 BLEU 分數
bleu_score, precisions, bp, ratio, translation_length, reference_length = compute_bleu(reference_corpus, translation_corpus)

# 輸出結果
print(f"BLEU score (BLEU 分數): {bleu_score}")
print(f"Precisions (精確度): {precisions}")
print(f"Brevity Penalty (簡短懲罰): {bp}")
print(f"Length Ratio (長度比): {ratio}")
print(f"Translation Length (翻譯長度): {translation_length}")
print(f"Reference Length (參考長度): {reference_length}")

```

### 計算 ROUGE 分數
ROUGE 分數用於衡量翻譯結果與參考語料庫的相似度，分數越高表示翻譯質量越好。
```python
from rouge import rouge

# 準備假設語料庫和參考語料庫
hypotheses = [
    "這是一個測試",
    "另一個測試",
    "又一個例子",
    "更多的句子用於測試",
    "最後一個例句"
]

references = [
    "這是二個測試",
    "另一個測試",
    "又一個例子",
    "更多的句子用於測試",
    "最後一個例句"
]

# 計算 ROUGE 分數
rouge_scores = rouge(hypotheses, references)

# 輸出結果
print(f"ROUGE-1 F1 score (ROUGE-1 F1 分數): {rouge_scores['rouge_1/f_score']}")
print(f"ROUGE-1 Precision (ROUGE-1 精確度): {rouge_scores['rouge_1/p_score']}")
print(f"ROUGE-1 Recall (ROUGE-1 召回率): {rouge_scores['rouge_1/r_score']}")
print(f"ROUGE-2 F1 score (ROUGE-2 F1 分數): {rouge_scores['rouge_2/f_score']}")
print(f"ROUGE-2 Precision (ROUGE-2 精確度): {rouge_scores['rouge_2/p_score']}")
print(f"ROUGE-2 Recall (ROUGE-2 召回率): {rouge_scores['rouge_2/r_score']}")
print(f"ROUGE-L F1 score (ROUGE-L F1 分數): {rouge_scores['rouge_l/f_score']}")
print(f"ROUGE-L Precision (ROUGE-L 精確度): {rouge_scores['rouge_l/p_score']}")
print(f"ROUGE-L Recall (ROUGE-L 召回率): {rouge_scores['rouge_l/r_score']}")
```


## 說明各個指標的效果

### BLEU 分數

BLEU score (BLEU 分數): 衡量翻譯結果與參考語料庫的相似度，分數越高表示翻譯質量越好。

Precisions (精確度): 各個 n-gram 的精確度，表示翻譯中有多少 n-gram 與參考語料庫匹配。

Brevity Penalty (簡短懲罰): 懲罰過短的翻譯，確保翻譯不會因為過於簡短而獲得高分。

Length Ratio (長度比): 翻譯長度與參考長度的比值，用於計算簡短懲罰。

Translation Length (翻譯長度): 翻譯語料庫的總長度。

Reference Length (參考長度): 參考語料庫的總長度。


### ROUGE 分數

ROUGE-1 F1 score (ROUGE-1 F1 分數): 衡量翻譯結果與參考語料庫的相似度，考慮了精確度和召回率的調和平均數。

ROUGE-1 Precision (ROUGE-1 精確度): 衡量翻譯結果中有多少 1-gram 與參考語料庫匹配。

ROUGE-1 Recall (ROUGE-1 召回率): 衡量參考語料庫中有多少 1-gram 被翻譯結果覆蓋。

ROUGE-2 F1 score (ROUGE-2 F1 分數): 衡量翻譯結果與參考語料庫的相似度，考慮了精確度和召回率的調和平均數，針對 2-gram。

ROUGE-2 Precision (ROUGE-2 精確度): 衡量翻譯結果中有多少 2-gram 與參考語料庫匹配。

ROUGE-2 Recall (ROUGE-2 召回率): 衡量參考語料庫中有多少 2-gram 被翻譯結果覆蓋。

ROUGE-L F1 score (ROUGE-L F1 分數): 衡量翻譯結果與參考語料庫的相似度，考慮了精確度和召回率的調和平均數，針對最長公共子序列（LCS）。

ROUGE-L Precision (ROUGE-L 精確度): 衡量翻譯結果中有多少 LCS 與參考語料庫匹配。

ROUGE-L Recall (ROUGE-L 召回率): 衡量參考語料庫中有多少 LCS 被翻譯結果覆蓋。

