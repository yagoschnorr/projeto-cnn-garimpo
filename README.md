# CNN Garimpo — DenseNet121

Classificação de recortes de imagens de satélite da Amazônia em `sem_garimpo` ou `com_garimpo` com uma DenseNet121 pré-treinada no ImageNet. O projeto compara três condições de treino: base congelada, fine-tuning A (bloco denso 4) e fine-tuning B (blocos densos 3 e 4).

Trabalho da disciplina de Inteligência Computacional/Machine Learning, sobre transfer learning e fine-tuning.

## Dataset

[Dataset Amazonia Garimpo Binario](https://www.kaggle.com/datasets/leogrupioni/dataset-amazonia-garimpo-binario), de Leo Grupioni, no Kaggle. O download é feito pelo próprio notebook com `kagglehub`.

## Estrutura

```
projeto-cnn-garimpo/
├── README.md
├── requirements.txt
├── dados/                          # imagens (fora do git), exceto divisao_amostra.csv
└── modelos/                        # modelos .keras (fora do git)
```

## Execução

Instruções completas de download, execução e uso do modelo serão adicionadas ao fim do projeto.
