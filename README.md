# CMP617 — Sumarização de Texto com BitNet b1.58 e LoRA

Repositório do trabalho final da disciplina CMP617 (PPGC — UFRGS), que investiga
a capacidade do modelo BitNet b1.58 em tarefas de sumarização de texto, antes e
após fine-tuning com LoRA, em três datasets de domínios distintos.

## Descrição

O trabalho avalia o BitNet b1.58 (2B parâmetros, pesos ternários {-1, 0, 1}) nos
datasets SAMSum, MediaSum e QMSum, combinando métricas automáticas (ROUGE, BLEU,
METEOR, BERTScore) com avaliação qualitativa humana e via G-Eval (Gemini).
Adicionalmente, conduz-se um experimento de sumarização hierárquica para o QMSum,
investigando estratégias para mitigar a perda de contexto em transcrições longas.

## Estrutura do Repositório
```
CMP617_BitNet_LoRA_Summarization/
├── SAMSum/                # Fine-tuning e análise do SAMSum
├── MediaSum/              # Fine-tuning e análise do MediaSum
├── QMSum/                 # Fine-tuning, análise e experimento hierárquico do QMSum
├── G_Eval/                # Avaliação automática via G-Eval (Gemini)
├── Graphs/                # Geração de gráficos de barras e boxplot
├── Summary_Visualizer/    # Visualização qualitativa dos resumos gerados
└── data/                  # CSVs de avaliação das 40 amostras por dataset
```

## Ordem de Execução

Para reproduzir os experimentos, execute os notebooks na seguinte ordem:

### SAMSum
1. `SAMSum/SAMSum_LoRA_FineTuning.ipynb`
2. `SAMSum/SAMSum_LoRA_Analysis_Baseline.ipynb`
3. `SAMSum/SAMSum_LoRA_Analysis_FT.ipynb`

### MediaSum
1. `MediaSum/MediaSum_LoRA_FineTuning.ipynb`
2. `MediaSum/MediaSum_LoRA_Analysis_Baseline.ipynb`
3. `MediaSum/MediaSum_LoRA_Analysis_FT.ipynb`

### QMSum
1. `QMSum/QMSum_LoRA_FineTuning.ipynb`
2. `QMSum/QMSum_LoRA_Analysis_Baseline.ipynb`
3. `QMSum/QMSum_LoRA_Analysis_FT.ipynb`

#### Sumarização Hierárquica (experimento complementar)
4. `QMSum/QMSum_LoRA_Strat_Sum_Base_Analysis.ipynb`
5. `QMSum/QMSum_LoRA_Strat_Sum_SAMSum_Analysis.ipynb`
6. `QMSum/QMSum_LoRA_Strat_Sum_MediaSum_Analysis.ipynb`
7. `QMSum/QMSum_LoRA_Strat_Sum_SAMSum_QMSUM_FT_Analysis.ipynb`

### G-Eval (após gerar os CSVs de avaliação)
- `G_Eval/g_eval_gemini_*.ipynb` — um notebook por dataset e condição

### Visualização
- `Graphs/` — gráficos de barras e boxplot das dimensões qualitativas
- `Summary_Visualizer/` — visualização comparativa dos resumos gerados

## Configuração

### Ambiente recomendado

Os notebooks foram desenvolvidos e testados no **Google Colab** com GPUs L4 e A100.
A execução local é possível, mas requer GPU com suporte a bfloat16.

### Dependências

```bash
pip install -r requirements.txt
```

### Chave de API — G-Eval

Os notebooks da pasta `G_Eval/` utilizam a API do Google Gemini. Configure sua
chave diretamente na variável indicada em cada notebook:

```python
GEMINI_API_KEY = "sua_chave_aqui"
```

### Dados

Os CSVs das 40 amostras de avaliação por dataset estão disponíveis na pasta `data/`.
Os arquivos de resultados completos (resumos gerados para os test sets completos)
não estão versionados devido ao tamanho — eles são gerados automaticamente ao
executar os notebooks de análise.

## Modelo

- **Modelo base:** `microsoft/bitnet-b1.58-2B-4T-bf16` (Hugging Face)
- **Técnica de fine-tuning:** LoRA (r=16, alpha=32, dropout=0.05,
  target_modules: q/k/v/o_proj)

## Citação

```bibtex
@misc{aragao2026bitnet,
  title  = {Sumarização de Texto com BitNet b1.58 e LoRA},
  author = {Aragão, Erhon L.},
  year   = {2026},
  note   = {Trabalho Final --- CMP617, PPGC/UFRGS}
}
```

## Orientação

- **Orientador:** Gabriel Nazar
- **Professores:** Viviane Moreira e Dennis Balreira
- **Programa:** PPGC — UFRGS, 2026
