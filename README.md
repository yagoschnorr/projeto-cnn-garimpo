# CNN Garimpo — DenseNet121

Classificação de recortes de imagens de satélite da Amazônia em `sem_garimpo` ou `com_garimpo` com uma DenseNet121 pré-treinada no ImageNet. O projeto compara três condições de treino: base congelada, fine-tuning A (bloco denso 4) e fine-tuning B (blocos densos 3 e 4), cada uma em cinco sementes (42 a 46).

Trabalho da disciplina de Inteligência Computacional/Machine Learning, sobre transfer learning e fine-tuning.

## Dataset

[Dataset Amazonia Garimpo Binario](https://www.kaggle.com/datasets/leogrupioni/dataset-amazonia-garimpo-binario), de Leo Grupioni, no Kaggle. O download é feito pelo próprio notebook com `kagglehub` (cerca de 3 GB, em `dados/kaggle/`). Se o Kaggle pedir credenciais, use o `kaggle.json` da sua conta, que nunca deve entrar no repositório.

## Estrutura

```
projeto-cnn-garimpo/
├── README.md
├── requirements.txt
├── cnn_garimpo_densenet121.ipynb   # notebook único
├── dados/
│   ├── divisoes/                   # divisao_semente_<semente>.csv (versionados)
│   └── kaggle/                     # imagens (fora do git)
├── modelos/                        # modelos .keras (fora do git)
├── resultados/                     # históricos JSON e tabelas (versionados)
└── rapido/                         # saídas do MODO_RAPIDO (fora do git)
```

## Ambiente

Python 3.11, TensorFlow 2.21 e Keras 3.15, as versões em que os modelos foram salvos. Versões diferentes podem não abrir os arquivos `.keras`.

```bash
python -m venv .venv
source .venv/bin/activate        # Windows: .venv\Scripts\activate
pip install -r requirements.txt
```

- **GPU NVIDIA (Linux ou WSL2):** instale `tensorflow[and-cuda]==2.21.*`. Se o sistema tiver um CUDA antigo e o TensorFlow não achar a GPU, crie um `.env` (fora do git) que aponte `LD_LIBRARY_PATH` para `.venv/lib/python3.11/site-packages/nvidia/nvjitlink/lib`.
- **Windows nativo:** o TensorFlow não usa GPU nessa versão. Use WSL2, Colab ou Kaggle Notebooks.
- **Colab:** escolha uma GPU, instale as dependências e monte o Google Drive para guardar `modelos/` e `resultados/` fora da sessão, que pode cair.

A primeira célula de código imprime as versões e a GPU encontrada. Confira que a lista de GPU não está vazia antes de treinar.

## Modelos

Os arquivos `.keras` ficam em `modelos/` e não vão para o git (cerca de 30 MB cada, 15 no total):

- `base_congelada_s<semente>.keras`
- `fine_tuning_a_s<semente>.keras`
- `fine_tuning_b_s<semente>.keras`

Eles estão na pasta compartilhada da equipe. Quem treina um modelo novo sobe o arquivo para lá.

## Como rodar o notebook

1. Abra `cnn_garimpo_densenet121.ipynb` e execute as células em ordem.
2. **Treinos já feitos são pulados.** Se o `.keras` de uma condição e semente já está em `modelos/`, o notebook carrega o histórico de `resultados/` em vez de treinar de novo. **Não retreine a base congelada**: os números e as análises do notebook são dos arquivos existentes.
3. **`MODO_RAPIDO`**, na célula de bibliotecas, vem como `False`. Com `True`, o notebook usa 200 imagens por divisão, 1 época por treino e só as sementes 42 e 43, e grava em `rapido/`. Serve para conferir que todas as células executam, sem esperar horas. Volte para `False` antes da execução final.
4. Cada treino de fine-tuning leva de 15 a 30 minutos por semente numa RTX 3060, e cerca do dobro numa T4 do Colab.

## Uso do modelo salvo

Instruções para carregar o modelo recomendado e classificar uma imagem nova serão adicionadas ao fim do projeto.
