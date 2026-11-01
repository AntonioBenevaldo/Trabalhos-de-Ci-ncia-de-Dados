# GlobalStream — retenção e segmentação de clientes

**Aluno:** Antônio Benevaldo Chaves Santana  
**Disciplina:** Introduction to Machine Learning — Ciência de Dados — UniFECAF  
**Revisão:** 24 de outubro de 2026

O projeto analisa a planilha fornecida com 1.000 clientes, identifica perfis com K-Means/PCA e compara classificadores do churn registrado. A base não tem datas nem histórico mensal; não há previsão temporal validada para o próximo mês.

## Comece aqui

1. Extraia todo o ZIP para uma pasta do computador. Não execute arquivos de dentro do ZIP.
2. Leia `Relatorio_GlobalStream_Revisado.docx`. Preencha o professor na capa e confira seus dados.
3. Use `Roteiro_e_Conferencia_GlobalStream.docx` para ensaiar o vídeo de até 4 minutos.
4. Para ver os gráficos sem executar Python, abra `GlobalStream_Visualizacao.html` no navegador. É uma visualização estática da execução; alterações no notebook não atualizam o HTML automaticamente.
5. Grave e publique o vídeo em modo não listado (ou plataforma compatível), teste o acesso ao link e coloque-o no final do Word.
6. Exporte novamente o Word para PDF e entregue o PDF final, o notebook e o link do vídeo. O PDF incluído neste pacote ainda tem campos pendentes de professor e vídeo. GitHub não é obrigatório pelo enunciado.

## Executar no Windows com Python 3.14

Abra o terminal na pasta extraída. Se o Python 3.14 estiver instalado e disponível pelo launcher `py`, execute um comando por vez:

```powershell
py -3.14 -m venv .venv
.\.venv\Scripts\python.exe -m pip install --upgrade pip
.\.venv\Scripts\python.exe -m pip install -r requirements.txt
.\.venv\Scripts\python.exe -m notebook GlobalStream_Churn.ipynb
```

No Jupyter, selecione **Kernel → Restart Kernel and Run All Cells** (reiniciar o kernel e executar todas as células). A validação cruzada aninhada faz muitos ajustes; a duração depende do computador. Mantenha `globalstream_data.xlsx` na mesma pasta do notebook. Se necessário, a célula de carregamento oferece um seletor de arquivos no Windows ou aceita o caminho completo em `ARQUIVO_EXCEL`.

Esta revisão foi executada em **Linux, Python 3.12.14**, em sessão IPython nova, com pandas 2.2.3, scikit-learn 1.8.0, NumPy 2.3.5, SciPy 1.17.0, Matplotlib 3.10.8 e openpyxl 3.1.5. Windows/Python 3.14 **não foram testados nesta revisão**. As instruções acima são um procedimento de instalação; confirme a execução no seu computador antes de gravar. As dependências de `requirements.txt` são faixas de versão, não uma garantia de números idênticos em qualquer ambiente. As versões efetivamente usadas ficam em `resultados/resultados.json`.

No Google Colab, abra o notebook, execute as células em ordem e envie a planilha quando solicitado. Esse ambiente não foi testado nesta revisão.

## Conteúdo

- `GlobalStream_Churn.ipynb`: código, gráficos, tabelas e interpretações; saídas regeneradas na revisão.
- `GlobalStream_Visualizacao.html`: visualização do notebook com os gráficos já calculados.
- `globalstream_data.xlsx`: planilha original preservada.
- `requirements.txt`: dependências para instalação.
- `Relatorio_GlobalStream_Revisado.docx` e `.pdf`: relatório técnico para completar a identificação e o link do vídeo.
- `Roteiro_e_Conferencia_GlobalStream.docx`: conferência do enunciado, roteiro de fala e orientações para mostrar os resultados.
- `resultados/`: figuras, métricas, partições, perfis, lista exploratória e registro das verificações.

## Resultados principais

| Item | Resultado |
|---|---|
| Base | 1.000 clientes, 54,2% com churn; treino 800 e teste 200 |
| Qualidade | Sem ausências ou duplicatas; nenhum outlier detectado no treino por IQR ou escore z |
| Segmentação | 6 grupos; silhouette 0,293, separação moderada a fraca |
| PCA | Duas componentes preservam 68,7% da variância |
| Modelo selecionado | Gradient Boosting; AUC CV aninhada 0,977 e AUC teste 0,982 |
| Limiar 0,50 | 103 VP, 7 FP, 5 FN e 85 VN; acurácia 94,0% |
| Limiar 0,17 | 108 VP, 21 FP, 0 FN e 71 VN; precisão 83,7%, recall 100%, acurácia 89,5% |
| Custo ilustrativo | De 811,90 para 482,32 u.m., redução de 40,6% sob as premissas do exercício |

AUC não é acurácia. Recall de 100% nesta amostra não garante 100% em novos clientes. A redução de custo é simulada e não representa economia efetiva ou cancelamentos evitados.

## Correções desta revisão

- Removidas alegações sem comprovação de execução em múltiplos sistemas e versões do Python.
- Corrigida a descrição de G1 e G2: diferem em contrato e frequência, embora ambos estejam abaixo da média de uso.
- Ajustadas conclusões sobre fidelidade, contrato, diferenças entre grupos e ações de retenção para respeitar o caráter associativo dos resultados.
- Cálculo de custos agora rejeita mensalidades ausentes, não finitas ou não positivas, evitando resultados silenciosamente inválidos.
- Acrescentadas duas verificações para o custo, totalizando 16.
- Removido o GitHub como pendência obrigatória e preparado roteiro alinhado ao limite de 4 minutos.
