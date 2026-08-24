## UNIDADE 2: DASHBOARD EXECUTIVO NO EXCEL (ANÁLISE E VISUALIZAÇÃO DE ACIDENTES PRF)

### Objetivo
Atuar como Analista de Dados sênior para transformar dados brutos em um **Relatório Visual Executivo (Dashboard)** no Excel, aplicando fórmulas avançadas, estatísticas descritivas e elementos visuais de alto impacto.

### O que foi feito:

#### Parte 1: Organização e Limpeza de Dados (Função SE e Operações)
1. **Cálculo de Vítimas Não Fatais:** Criada a coluna `Vítimas Feridas` usando subtração:
   ```
   = [pessoas] - [mortos] - [ilesos] - [ignorados]
   ```
2. **Classificação de Gravidade:** Criada a coluna `Status de Fatalidade` com a função `=SE()`:
   ```
   =SE([mortos] > 0; "Crítico"; "Sem Vítimas Fatais")
   ```

#### Parte 2: Proporções e Desempenho
3. **Cálculo de Proporção:** Criada a coluna `Taxa de Feridos Graves`:
   ```
   = [feridos_graves] / [pessoas]
   ```
   (Formatada como porcentagem)
4. **Fator de Impacto por Veículo:** Criada a coluna `Pontuação de Risco`:
   ```
   = [veiculos] * 10
   ```

#### Parte 3: Parâmetros Estatísticos
Em uma nova aba, foi criada a seção "Resumo Estatístico" com:
5. **Média:** `=MÉDIA([veiculos])` - número médio de veículos por acidente.
6. **Mediana:** `=MED([pessoas])` - ponto central de envolvidos.
7. **Quartil:** `=QUARTIL.INC([pessoas]; 3)` - terceiro quartil da distribuição.

#### Parte 4: Motor de Busca de Acidentes (PROCV)
8. **Painel de Consulta Rápida:** Criação de uma tabela onde, ao digitar o ID do acidente, o Excel preenche automaticamente:
   - Município do acidente
   - Causa do acidente
   - Condição Meteorológica
   
   Utilizando a fórmula:
   ```
   =PROCV(ID; tabela_dados; coluna; FALSO)
   ```

#### Parte 5: Consolidação e Contagens
9. **Contagem Total:** `=CONT.VALORES([id])` para registrar o total de acidentes.
10. **Filtro de Região:** `=CONT.SE([uf]; "SP")` e `=CONT.SE([uf]; "PE")` para contar acidentes nesses estados.

#### Parte 6: Gráfico de Dispersão (Correlação)
11. **Relação entre Veículos e Pessoas:**
    - Selecionadas as colunas `[veiculos]` e `[pessoas]`.
    - Inserido **Gráfico de Dispersão (X,Y)**.
    - Adicionada **Linha de Tendência** para avaliar visualmente a correlação entre as variáveis.
    - **Conclusão:** Quanto maior o número de veículos, maior tende a ser o número de pessoas envolvidas.

#### Parte 7: Gráfico de Rosca ou Pizza (Composição)
12. **Distribuição da Fase do Dia:**
    - Criada tabela auxiliar com contagem de acidentes por fase do dia usando `CONT.SE`.
    - Inserido **Gráfico de Rosca** com rótulos de dados formatados como porcentagem.
    - **Conclusão:** "Pleno dia" concentra o maior volume de acidentes, mas "Plena Noite" tem maior letalidade.

#### Parte 8: Gráfico de Barras Horizontais (Comparação de Categorias)
13. **Ranking de Causas de Acidentes:**
    - Tabela auxiliar listando as 5 principais causas e suas quantidades.
    - Inserido **Gráfico de Barras Horizontais** com ordenação decrescente.
    - **Conclusão:** "Ausência de reação do condutor" é a causa mais frequente, seguida por "Reação tardia ou ineficiente".

#### Parte 9: Gráfico de Linhas (Tendência Temporal)
14. **Evolução Mensal de Acidentes:**
    - Contagem agrupada de acidentes mês a mês.
    - Inserido **Gráfico de Linhas** com marcadores.
    - **Conclusão:** Maio, Junho e Dezembro apresentam os picos de acidentes.

#### Parte 10: Gráfico de Colunas Empilhadas (Análise Cruzada)
15. **Condição Meteorológica por Estado:**
    - Tabela de dupla entrada cruzando estados (SP, PE, MG) e condições do tempo (Céu Claro, Chuva).
    - Inserido **Gráfico de Colunas Empilhadas**.
    - **Conclusão:** "Céu Claro" é a condição mais frequente em todos os estados analisados, seguida por "Chuva".

#### Critérios de Entrega Atendidos:
- **Interatividade:** Gráficos e painel PROCV são dinâmicos.
- **Design Limpo:** Remoção de linhas de grade, títulos claros e paleta de cores profissional.

---
