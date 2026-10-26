# Processamento Digital de Imagens (PDI)

Repositório dedicado ao desenvolvimento das atividades práticas da disciplina de **Processamento Digital de Imagens (PDI)**.

* **Tema do Trabalho:** Gastronomia
* **Gerenciador de Dependências:** [`uv`](https://github.com/astral-sh/uv)
* **Ambiente de Desenvolvimento:** Python 3.13 / Jupyter Notebook

---

## 📚 Estrutura das Atividades (1 de 4)

Este repositório está organizado em uma série de **4 atividades práticas**:

| Atividade | Arquivo | Descrição | Status |
| :--- | :--- | :--- | :---: |
| **Atividade 1** | [`Atividade_1_PDI.ipynb`](./Atividade_1_PDI.ipynb) | Fundamentos, Transformações de Intensidade e Espaciais Manuais | ✅ Concluída |
| **Atividade 2** | [`Atividade_2_PDI.ipynb`](./Atividade_2_PDI.ipynb) | Transformações no Domínio Espacial ($h_1$ a $h_{11}$) e Domínio da Frequência (FFT, Filtros Espectrais e Compressão) | ✅ Concluída |
| **Atividade 3** | `Atividade_3_PDI.ipynb` | *(Em breve)* | ⏳ Pendente |
| **Atividade 4** | `Atividade_4_PDI.ipynb` | *(Em breve)* | ⏳ Pendente |

---

## 🔬 Atividade 1: Implementação Manual de Técnicas Clássicas

O primeiro notebook ([`Atividade_1_PDI.ipynb`](./Atividade_1_PDI.ipynb)) aborda a implementação manual de algoritmos clássicos de PDI via **NumPy**, restringindo o OpenCV apenas para entrada/saída e desfoque gaussiano onde solicitado:

1. **Questão 1 — Efeito de Esboço a Lápis (*Pencil Sketch*):** Conversão manual para níveis de cinza (ITU-R BT.601), suavização passa-baixas com filtro gaussiano $21 \times 21$ e divisão matricial para realce de bordas (*Color Dodge Blend*).
2. **Questão 2 — Correção Gama:** Transformação de lei de potência não-linear ($B = A^{1/\gamma}$) com análise de curvas de transferência e histogramas de contraste.
3. **Questão 3 — Combinação Ponderada de Imagens (*Alpha Blending*):** Interpolação linear convexa $I_{\text{blend}} = \alpha I_1 + (1 - \alpha) I_2$ com preservação de faixa dinâmica.
4. **Questão 4 — Transformações de Intensidade e Geométricas:**
   - (b) Negativo da imagem ($255 - I$);
   - (c) Compressão de contraste para o intervalo $[100, 200]$;
   - (d) Inversão horizontal seletiva das linhas pares ($y \pmod 2 = 0$);
   - (e) Espelhamento da metade superior na parte inferior;
   - (f) Espelhamento vertical total (*flip vertical*).
5. **Questão 5 — Mosaico $4 \times 4$ de Blocos Permutados:** Particionamento espacial uniforme e permutação determinística com reconstrução inversa sem perdas (*lossless*).
6. **Questão 6 — Quantização de Níveis de Cinza:** Discretização radiométrica de $8$ a $1$ bits com avaliação quantitativa de PSNR/RMSE e análise de falsos contornos (*banding*) e posterização.

---

## 🔬 Atividade 2: Transformações Espaciais e no Domínio da Frequência

O segundo notebook ([`Atividade_2_PDI.ipynb`](./Atividade_2_PDI.ipynb)) aborda a filtragem espacial linear com os 11 kernels solicitados e a filtragem/compressão espectral com a Transformada Rápida de Fourier (FFT 2D):

1. **Questão 1 — Filtragem no Domínio Espacial (Kernels $h_1$ a $h_{11}$):**
   - Convolução discreta bidimensional implementada manualmente via NumPy com inversão de 180° e padding reflexivo;
   - Implementação exata dos 11 filtros: Laplaciano $5\times 5$ ($h_1$), Gaussiano binomial $5\times 5$ ($h_2$), Sobel vertical $3\times 3$ ($h_3$), Sobel horizontal $3\times 3$ ($h_4$), Laplaciano $3\times 3$ de 8 vizinhos ($h_5$), média móvel $3\times 3$ ($h_6$), detectores direcionais de linhas a $\pm 45^\circ$ ($h_7$, $h_8$), *motion blur* diagonal $9\times 9$ ($h_9$), realce passa-altas *high-boost* $5\times 5$ ($h_{10}$) e filtro de entalhe/relevo pseudo-3D *emboss* ($h_{11}$);
   - Normalização adequada da faixa dinâmica e inspeção detalhada em ROI.
2. **Questão 2 — Transformada de Fourier, Filtragem Espectral e Compressão:**
   - Centralização de espectro com componente DC no centro geométrico (`fftshift`) e representação logarítmica;
   - Construção manual das máscaras analíticas dos 4 filtros ideais: Passa-Baixa (ILPF), Passa-Alta (IHPF), Passa-Faixa (IBPF) e Rejeita-Faixa (IBRF);
   - Estudo comparativo de raios de corte ($D_0$) e análise do efeito de anelamento (*ringing artifact*) com filtro de Butterworth;
   - Compressão no domínio da frequência por limiarização de magnitude dos coeficientes (taxas de esparsidade de 90%, 95%, 97% e 99%), cálculo de métricas objetivas (PSNR e MSE) e comparação dos histogramas antes e após a compressão.

---

## 🚀 Como Executar o Projeto

Este projeto utiliza o **`uv`** para gerenciamento rápido e determinístico de dependências.

### 1. Clonar o Repositório
```bash
git clone https://github.com/kaynanxd/Processamento-de-imagens.git
cd Processamento-de-imagens
```

### 2. Abrir o Jupyter Lab / Notebook
O `uv` sincronizará automaticamente todas as dependências isoladas no ambiente virtual:
```bash
uv run jupyter lab
# ou
uv run jupyter notebook
```

### 3. Gerar o Notebook e o PDF

O gerador executa todas as células e cria automaticamente o notebook e sua
versão em PDF. É necessário ter Microsoft Edge ou Google Chrome instalado.

### Gerar as versões individuais editáveis e PDFs
```bash
# Atividade 1:
uv run python scripts/generate_atividade_1_notebook.py

# Atividade 2:
uv run python scripts/generate_atividade_2_notebook.py
```
O script gera o notebook correspondente com todas as células executadas e seu respectivo arquivo PDF.

---

## 🍰 Dataset e Licença

As imagens temáticas utilizadas nos experimentos pertencem ao dataset de bolos e confeitaria criado por **Fülöp Bettina-Elena e Cristea Ioan (2019-2020)**, disponibilizado sob a **Licença MIT**:

```text
MIT License
Copyright (c) 2019-2020 Fülöp Bettina-Elena, Cristea Ioan
```
