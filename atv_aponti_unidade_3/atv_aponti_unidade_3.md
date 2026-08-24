## UNIDADE 3: MODELAGEM E CONSULTAS EM BANCO DE DADOS (SCRIPT SQL)

### Arquivos:
- `acidentes_por_br.csv`
- `acidentes_por_causa.csv`
- `acidentes_por_clima.csv`
- `acidentes_por_fase_dia.csv`
- `acidentes_por_mes.csv`
- `acidentes_por_tipo.csv`
- `acidentes_por_uf.csv`
- `script.sql`

### Objetivo
Criar uma estrutura de dados em SQL e realizar consultas analíticas para extrair insights aprofundados.

### O que foi feito:

#### 1. Criação da View Base (`vw_acidentes_base`)
Adicionada a coluna `acidente_fatal`:
```sql
CASE 
    WHEN mortos >= 1 THEN 1
    ELSE 0
END AS acidente_fatal
```

#### 2. Indicadores Gerais
- Total de acidentes: `COUNT(*)`
- Total de fatais: `SUM(acidente_fatal)`
- Percentual de letalidade: `ROUND((SUM(acidente_fatal) * 100.0) / COUNT(*), 2)`

#### 3. Análises por Dimensão
- **UF:** Estados com maior e menor percentual de letalidade.
- **BR:** Rodovias com maior número absoluto de mortos.
- **Tipo de Acidente:** Comparação da letalidade entre diferentes tipos.
- **Fase do Dia:** Avaliação do impacto do horário na gravidade.
- **Clima:** Análise da influência das condições meteorológicas.
- **Tipo de Pista:** Comparação da segurança em pistas simples, duplas ou múltiplas.

#### 4. Análise de "Lift"
Cálculo do quão mais letal um tipo de acidente é em relação à média geral:
```sql
WITH media_geral AS (
    SELECT (SUM(acidente_fatal) * 1.0 / COUNT(*)) AS taxa_media
    FROM vw_acidentes_base
)
SELECT 
    tipo_acidente,
    ROUND((SUM(acidente_fatal) * 1.0 / COUNT(*)) / media_geral.taxa_media, 2) AS lift
FROM vw_acidentes_base, media_geral
GROUP BY tipo_acidente
ORDER BY lift DESC;
```

#### 5. Criação de Views para Dashboards
- `vw_indicadores_mensais:` Visão temporal por ano/mês.
- `vw_indicadores_uf_br:` Visão geográfica por estado e rodovia.
- `vw_dashboard_acidentes:` View consolidada com todas as dimensões e métricas.

### Principais Insights Extraídos:
- **Atropelamentos de pedestres** são os tipos mais letais (Lift > 5).
- **Estados como MA, PA e RR** apresentam as maiores taxas de letalidade.
- **BR-101 e BR-116** concentram o maior número de mortes.
- **Plena Noite e Amanhecer** têm maior letalidade.
- **Céu Claro e Chuva** são as condições mais frequentes, mas "Nevoeiro" tem a maior taxa de letalidade.

---
