# 📊 Projeto – Análise de Investimentos em Renda Fixa (5 Anos)
<img width="638" height="355" alt="image" src="https://github.com/user-attachments/assets/8551358f-ed63-4c13-9c01-b0bee8c93b4e" />

Recentemente, em uma conversa com alguns amigos sobre investimentos, surgiu uma pergunta que dividiu opiniões:

> **Qual investimento é o melhor a longo prazo?**

As respostas vieram cheias de achismos, informações falsas ou desatualizadas, e nenhuma conclusão concreta foi alcançada. Isso despertou algumas dúvidas importantes:

- Qual investimento rende mais ao longo dos anos?
- Onde devo investir meu dinheiro?
- Vale a pena correr mais risco ou investir em algo mais seguro?
- No Brasil, como o Imposto de Renda impacta esses investimentos?

Com base nessas perguntas, decidi criar este projeto utilizando **Python + Power BI** para analisar dados reais e trazer respostas mais objetivas.

---

## 📌 O que é investimento de renda fixa?

Segundo o Gemini, investimentos de renda fixa são aqueles em que você sabe (ou tem uma fórmula para saber) quanto irá receber no futuro no momento da aplicação.

Basicamente, você está:
- Emprestando dinheiro para o Governo (Tesouro)
- Ou para bancos/empresas (CDB, LCI, LCA, etc.)

---

## 💰 Investimentos Analisados

### 1️⃣ Tesouro Selic

**Como funciona:**  
Você empresta dinheiro ao Governo Federal, que remunera pela Taxa Selic.

- Rentabilidade típica: 100% da Selic (próximo ao CDI)
- Risco: Extremamente baixo (benchmark de segurança do país)

---

### 2️⃣ Investimentos Bancários (CDB, LCI/LCA)

#### CDB – Certificado de Depósito Bancário

- O que é: Título emitido por bancos para captação de recursos
- Rentabilidade típica: 100% a 120% do CDI
- IR: Incide Imposto de Renda

#### LCI / LCA

- O que é: Títulos para financiar os setores imobiliário e agrícola
- Rentabilidade típica: 90% a 95% do CDI
- IR: Isento

**Risco Principal:**  
Risco de crédito (quebra do banco).  
Todos contam com garantia do FGC até R$ 250 mil por CPF e por instituição.

---

### 3️⃣ Bancos Digitais e “Caixinhas”

#### Caixinhas (Nubank, etc.)

- Fundos DI simples
- Investem em Tesouro Selic ou CDBs
- Rentabilidade típica: ~100% do CDI
- Não possuem FGC (são fundos), mas o risco é baixo

#### Rendimento em Conta (Mercado Pago, 99Pay, etc.)

- Normalmente CDB de liquidez diária
- Rentabilidade varia (ex: Mercado Pago paga 100% do CDI após 30 dias)
- Possuem FGC quando o CDB está no seu CPF

---

### 4️⃣ Comparação de Rendimento Mensal (Foco no CDI)

Os investimentos de liquidez diária tendem a ter rentabilidade bruta muito parecida, pois seguem o CDI diário.

As diferenças estão em:
- Carência
- Incidência de IR
- Regras específicas de cada banco

Por isso, foi considerado CDI = 100% como padrão.

---

## 📅 Período Analisado

- 01/01/2020 até 05/12/2025  
- Aproximadamente 5 anos

---

## ⚙️ Premissas do Projeto

- CDI considerado sempre em 100%
- CDI 120% analisado como cenário adicional
- Alíquota de IR: 15% (prazo acima de 5 anos)
- LCI/LCA: 90% do CDI e isento de IR
- Dados reais do Banco Central do Brasil

---

## 🐍 Python – Engenharia de Dados

O Python foi responsável por toda a parte de engenharia e simulação financeira.

### Principais etapas:

- **Busca de dados reais:**  
  Utilização da biblioteca `bcb` para coletar CDI e Selic diários diretamente do Banco Central.

- **Simulação financeira:**  
  Aplicação da lógica de rentabilidade diária para Tesouro Selic, CDB e LCI/LCA, incluindo o desconto de IR (15% sobre o lucro).

- **Modelagem de tempo:**  
  Criação de uma Tabela Calendário limpa para viabilizar os cálculos no Power BI via DAX.

> Observação: este projeto representa um recorte de um código maior.

---

## 📊 Power BI – Visualização e Análise

### Etapas realizadas:

- Importação da tabela calendário (CSV gerada no Python)
- Criação das medidas em DAX
- Construção dos gráficos e layout final
- Design das imagens feito no Figma

---

## 🧮 Principais Medidas DAX (Exemplo)

```DAX
Lucro_TS_LIQUIDO =
MAX(analise_renda_fixa_5_anos[Saldo_Liquido_TS]) - 1000

Lucro_TS_BRUTO =
MAX(analise_renda_fixa_5_anos[Saldo_Liquido_TS])

%YoY TS =
VAR AnoAnterior =
    CALCULATE(
        [Lucro_TS_LIQUIDO],
        DATEADD(Calendario[Date], -1, YEAR)
    )
VAR AnoAtual = [Lucro_TS_LIQUIDO]
RETURN
IF(
    ISBLANK(AnoAnterior),
    BLANK(),
    DIVIDE(AnoAtual - AnoAnterior, AnoAnterior)
)
```
As medidas foram replicadas para cada tipo de investimento.
📌 Resultados Finais (Lucro Líquido)

Todos os valores abaixo já consideram o desconto de 15% de IR.

Investimento	Lucro Líquido
CDI 120%	R$ 1.327,06
Tesouro Selic	R$ 1.025,38
LCI	R$ 1.024,69
CDI 100%	R$ 1.011,27

🧠 Conclusões
O CDI 120% foi o melhor investimento no cenário analisado
Porém, normalmente exige condições específicas (aporte mensal, regras do banco, etc.)

Desconsiderando o CDI 120%:
Tesouro Selic e LCI apresentaram resultados praticamente idênticos

Tesouro Selic se destaca pela segurança máxima

LCI se destaca pela isenção de IR

Conclusão final:
O melhor investimento depende do seu perfil e das condições disponíveis.

Cumpre as regras do CDI 120%? → Melhor opção

Quer simplicidade e segurança? → Tesouro Selic

📎 Contatos

LinkedIn: https://www.linkedin.com/in/cleiton-silveira21/

GitHub do Projeto: https://github.com/Cleitondev01/Projeto-Investimento-fixo-5-anos

Portfólio: https://cleitonsilveira-portfolio.lovable.app/
