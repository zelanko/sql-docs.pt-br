---
title: Estimativa de cardinalidade (SQL Server) | Microsoft Docs
description: O Otimizador de Consulta do SQL Server seleciona os planos de consulta com o menor custo de processamento estimado, que ele determina com base nas linhas processadas e em um modelo de custo.
ms.custom: ''
ms.date: 02/24/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- cardinality estimator
- CE (cardinality estimator)
- estimating cardinality
ms.assetid: baa8a304-5713-4cfe-a699-345e819ce6df
author: WilliamDAssafMSFT
ms.author: wiassaf
monikerRange: =azuresqldb-current||>=sql-server-2016||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: f2d814c604ac742723fc1fb9c7e3c12dc375884f
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97417975"
---
# <a name="cardinality-estimation-sql-server"></a>Estimativa de cardinalidade (SQL Server)

[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]

O Otimizador de Consulta do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é baseado em custo. Isso significa que ele seleciona planos de consulta com o custo de processamento estimado mais baixo para ser executado. O Otimizador de Consulta determina o custo de execução de um plano de consulta com base em dois fatores principais:

- O número total de linhas processadas em cada nível de um plano de consulta, chamado cardinalidade do plano.
- O modelo de custo do algoritmo ditado pelos operadores usados na consulta.

O primeiro fator, cardinalidade, é usado como um parâmetro de entrada do segundo fator, o modelo de custo. Portanto, a cardinalidade aprimorada gera custos melhor estimados e, consequentemente, planos de execução mais rápidos.

A CE (estimativa de cardinalidade) em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é derivada principalmente de histogramas criados quando índices ou estatísticas são criados, manual ou automaticamente. Às vezes, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] também usa informações de restrição e novas consultas lógicas para determinar a cardinalidade.

Nos casos a seguir, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não consegue calcular cardinalidades com precisão. Isso gera cálculos de custo inexatos que podem causar planos de consulta menos favoráveis. Evitando-se tais construções em consultas é possível melhorar o desempenho da consulta. Às vezes, formulações de consulta alternativas ou outras medidas são possíveis e são indicadas:

- Consultas com predicados que usam operadores de comparação entre colunas diferentes da mesma tabela.
- Consultas com predicados que usam operadores e qualquer um dos itens seguintes são true:
  - Não há nenhuma estatística referente às colunas envolvidas em nenhum dos lados dos operadores.
  - A distribuição de valores nas estatísticas não é uniforme, mas a consulta busca um conjunto de valores altamente seletivo. Essa situação pode ser especialmente verdadeira se o operador não for o operador de igualdade (=).
  - O predicado usa o operador de comparação diferente de (! =) ou o operador lógico `NOT`.
- Consultas que usem qualquer uma das funções internas do SQL Server ou uma função com valor escalar, definida pelo usuário, cujo argumento não é um valor constante.
- Consultas que envolvem colunas de associação por aritmética ou operadores de concatenação de cadeias de caracteres.
- Consultas que comparam variáveis cujos valores não são conhecidos quando a consulta é compilada e otimizada.

Este artigo ilustra como você pode avaliar e escolher a melhor configuração de CE para seu sistema. A maior parte dos sistemas se beneficia da CE mais recente, pois ela é a mais precisa. A CE prevê o número de linhas que sua consulta provavelmente retornará. A previsão de cardinalidade é usada pelo Otimizador de Consulta para gerar o plano de consulta ideal. Com estimativas mais precisas, o Otimizador de Consulta normalmente pode fazer um trabalho melhor de produção de um plano de consulta melhor.  
  
Seu sistema de aplicativos poderia ter uma consulta importante cujo plano foi alterado para um plano mais lento devido às alterações na CE ao longo das versões. Você tem técnicas e ferramentas para identificar uma consulta com desempenho mais lento devido a problemas na CE. Além disso, você tem opções para resolver problemas de desempenho decorrentes disso.
  
## <a name="versions-of-the-ce"></a>Versões da CE

Em 1998, uma importante atualização da CE fez parte do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] 7.0, para o qual o nível de compatibilidade era 70. Essa versão do modelo da CE é definida em quatro suposições básicas:

-  **Independência:** as distribuições de dados em diferentes colunas são consideradas independentes entre si, a menos que haja informações de correlação disponíveis e elas sejam utilizáveis.
-  **Uniformidade:** diferentes valores são espaçados uniformemente e todos eles têm a mesma frequência. Mais precisamente, dentro de cada etapa de [histograma](../../relational-databases/statistics/statistics.md#histogram), diferentes valores são distribuídos uniformemente e cada valor tem a mesma frequência. 
-  **Independência (simples):** os usuários consultam dados existentes. Por exemplo, para uma junção de igualdade entre duas tabelas, considere a seletividade de predicados<sup>1</sup> em cada histograma de entrada antes de ingressar histogramas para estimar a seletividade da junção. 
-  **Inclusão:** para filtrar predicados em que `Column = Constant`, supõe-se que a constante realmente exista para a coluna associada. Se uma etapa do histograma correspondente não estiver vazia, presume-se que um dos valores diferentes da etapa corresponda ao valor do predicado.

  <sup>1</sup> Contagem de linhas que satisfaz o predicado.

Atualizações posteriores iniciadas com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], significando níveis de compatibilidade 120 e acima. As atualizações da CE dos níveis 120 e acima incorporam suposições e algoritmos atualizados que funcionam bem em data warehousing moderno e em cargas de trabalho OLTP. De suposições da CE 70, as seguintes suposições de modelo foram alteradas a partir da CE 120:

-  **Independência** torna-se **Correlação:** a combinação dos diferentes valores de coluna não é necessariamente independente. Isso poderia parecer mais com uma consulta de dados da vida real.
-  **Independência simples** torna-se **Independência de base:** Os usuários podem consultar dados que não existem. Por exemplo, para que haja uma junção de igualdade entre duas tabelas, usamos histogramas de tabelas básicos para calcular a seletividade da junção e, sem seguida, consideramos a seletividade de predicados.
  
**Nível de compatibilidade:** é possível garantir que o banco de dados esteja em determinado nível usando o seguinte código do [!INCLUDE[tsql](../../includes/tsql-md.md)] para [COMPATIBILITY_LEVEL](../../t-sql/statements/alter-database-transact-sql-compatibility-level.md).  

```sql  
SELECT ServerProperty('ProductVersion');  
GO  
  
ALTER DATABASE <yourDatabase>  
SET COMPATIBILITY_LEVEL = 130;  
GO  
  
SELECT d.name, d.compatibility_level  
FROM sys.databases AS d  
WHERE d.name = 'yourDatabase';  
GO  
```  
  
Para um banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido no nível de compatibilidade 120 ou superior, a ativação do [sinalizador de rastreamento 9481](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) força o sistema a usar a CE versão 70.  
  
**CE herdada:** Para obter um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] definido no nível de compatibilidade 120 e acima, a versão 70 do CE poderá ser ativada no nível do banco de dados usando [ALTER DATABASE SCOPED CONFIGURATION](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md).
  
```sql  
ALTER DATABASE SCOPED CONFIGURATION 
SET LEGACY_CARDINALITY_ESTIMATION = ON;  
GO  
  
SELECT name, value  
FROM sys.database_scoped_configurations  
WHERE name = 'LEGACY_CARDINALITY_ESTIMATION';  
GO
```  
 
Ou, então, no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 em diante, a [Dica de Consulta](../../t-sql/queries/hints-transact-sql-query.md#use_hint) `USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION')`.
 
 ```sql  
SELECT CustomerId, OrderAddedDate  
FROM OrderTable  
WHERE OrderAddedDate >= '2016-05-01'
OPTION (USE HINT ('FORCE_LEGACY_CARDINALITY_ESTIMATION'));  
```
 
**Repositório de Consultas:** Começando pelo [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], o Repositório de Consultas é uma ferramenta útil para examinar o desempenho das consultas. No [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], no **Pesquisador de Objetos**, no nó do seu banco de dados, um nó **Repositório de Consultas** é exibido quando o repositório de consultas está habilitado.  
  
```sql  
ALTER DATABASE <yourDatabase>  
SET QUERY_STORE = ON;  
GO  
  
SELECT q.actual_state_desc AS [actual_state_desc_of_QueryStore],  
        q.desired_state_desc,  
        q.query_capture_mode_desc  
FROM sys.database_query_store_options AS q;  
GO  
  
ALTER DATABASE <yourDatabase>  
SET QUERY_STORE CLEAR;  
```  
  
> [!TIP] 
> É recomendado instalar a versão mais recente do [Management Studio](../../ssms/download-sql-server-management-studio-ssms.md) e atualizá-lo com frequência.  

> [!IMPORTANT] 
> Verifique se a Repositório de Consultas está configurado corretamente para seu banco de dados e carga de trabalho. Para obter mais informações, consulte [Melhores práticas com Repositório de Consultas](../../relational-databases/performance/best-practice-with-the-query-store.md). 
  
Outra opção para acompanhar o processo de estimativa de cardinalidade é usar o evento estendido chamado **query_optimizer_estimate_cardinality**. O exemplo de código [!INCLUDE[tsql](../../includes/tsql-md.md)] a seguir é executado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Ele grava um arquivo .xel em `C:\Temp\` (embora o caminho possa ser alterado). Quando você abre o arquivo .xel no [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], as informações detalhadas são exibidas de forma amigável.  
  
```sql  
DROP EVENT SESSION Test_the_CE_qoec_1 ON SERVER;  
go  
  
CREATE EVENT SESSION Test_the_CE_qoec_1  
ON SERVER  
ADD EVENT sqlserver.query_optimizer_estimate_cardinality  
    (  
        ACTION (sqlserver.sql_text)  
            WHERE (  
                sql_text LIKE '%yourTable%'  
                and sql_text LIKE '%SUM(%'  
            )  
    )  
ADD TARGET package0.asynchronous_file_target   
        (SET  
            filename = 'c:\temp\xe_qoec_1.xel',  
            metadatafile = 'c:\temp\xe_qoec_1.xem'  
        );  
GO  
  
ALTER EVENT SESSION Test_the_CE_qoec_1  
ON SERVER  
STATE = START;  --STOP;  
GO  
```  
  
Para obter informações sobre eventos estendidos adaptados para o [!INCLUDE[ssSDS](../../includes/sssds-md.md)], veja [Eventos estendidos no Banco de Dados SQL](/azure/azure-sql/database/xevent-db-diff-from-svr).  
  
## <a name="steps-to-assess-the-ce-version"></a>Etapas para avaliar a versão da CE  
  
A seguir, veja as etapas que você pode usar para avaliar se qualquer uma das suas consultas mais importantes tem um desempenho inferior na CE mais recente. Algumas das etapas são realizadas com a execução de um exemplo de código apresentado em uma seção anterior.  
  
1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)]. Verifique se [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]banco de dados é definido como o mais alto nível de compatibilidade disponível.  
  
2.  Realize as seguintes etapas preliminares:  
  
    1.  Abra o [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)].  
  
    2.  Execute o T-SQL para garantir que o banco de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é definido com o nível de compatibilidade mais alto disponível.  
  
    3.  Verifique se o seu banco de dados tem a configuração `LEGACY_CARDINALITY_ESTIMATION` como OFF.  
  
    4.  Limpe seu Repositório de Consultas. Verifique se o Repositório de Consultas está ON.  
  
    5.  Execute a instrução: `SET NOCOUNT OFF;`  
  
3.  Execute a instrução: `SET STATISTICS XML ON;`  
  
4.  Execute a consulta importante.  
  
5.  No painel de resultados, na guia **Mensagens** , observe o número real de linhas afetadas.  
  
6.  No painel de resultados, na guia **Resultados** , clique duas vezes na célula que contém as estatísticas em formato XML. Um plano de consulta gráfico é exibido.  
  
7.  Clique com o botão direito do mouse na primeira caixa do plano de consulta gráfico e clique em **Propriedades**.  
  
8.  Para a comparação posterior com uma configuração diferente, observe os valores das seguintes propriedades:  
  
    -   **CardinalityEstimationModelVersion**.  
  
    -   **Número Estimado de Linhas**.  
  
    -   **Estimated I/O Cost** e várias propriedades *Estimated* semelhantes que envolvem o desempenho real em vez de previsões de contagem de linha.  
  
    -   **Operação Lógica** e **Operação Física**. *Parallelism* é um valor aceitável.  
  
    -   **Modo de Execução Real**. *Batch* é um valor aceitável, melhor que *Row*.  
  
9. Compare o número estimado de linhas com o número real de linhas. A CE não é precisa em % 1 (alto ou baixo) ou 10%?  
  
10. Execute: `SET STATISTICS XML OFF;`  
  
11. Execute o T-SQL para diminuir o nível de compatibilidade do banco de dados em um nível (por exemplo, 130 até 120).  
  
12. Execute novamente todas as etapas não preliminares.  
  
13. Compare os valores de propriedade da CE das duas execuções.  
  
    - O percentual de imprecisão na CE mais recente está abaixo da CE mais antiga?  
  
14. Por fim, compare vários valores de propriedade de desempenho das duas execuções.  
  
    -   Sua consulta usou um plano diferente nas duas estimativas de CE diferentes?  
  
    -   A consulta foi executada mais lentamente na CE mais recente?  
  
    -   A menos que a consulta tenha um desempenho melhor e com um plano diferente na CE mais antiga, certamente, será recomendável a CE mais recente.  
  
    -   No entanto, se sua consulta for executada com um plano mais rápido na CE mais antiga, considere forçar o sistema para usar o plano mais rápido e ignorar a CE. Dessa forma, você pode ter a CE mais recente para tudo, ao mesmo tempo que mantém o plano mais rápido por via das dúvidas.  
  
## <a name="how-to-activate-the-best-query-plan"></a>Como ativar o melhor plano de consulta  
  
Suponha que, com a CE 120 ou superior, um plano de consulta menos eficiente é gerado para sua consulta. Aqui estão algumas opções para ativar o plano melhor:  
  
1. Você pode definir o nível de compatibilidade de todo o seu banco de dados com um valor menor do que o valor mais recente disponível.  
  
   - Por exemplo, configurar o nível de compatibilidade 110 ou inferior ativa a CE 70, mas deixa todas as consultas sujeitas ao modelo de CE anterior.  
  
   - Além disso, configurar um nível de compatibilidade inferior também faz inúmeras melhorias no otimizador de consulta para as versões mais recentes serem perdidas.  
  
2. Você poderá usar a opção de banco de dados `LEGACY_CARDINALITY_ESTIMATION` para fazer com que todo o banco de dados use a CE mais antiga, mantendo outras melhorias no otimizador de consulta.   

3. Você poderá usar a dica de consulta `LEGACY_CARDINALITY_ESTIMATION` para fazer com que uma única consulta use a CE mais antiga, mantendo outras melhorias no otimizador de consulta.  
  
Para obter o controle mais refinado, você pode *forçar* o sistema a usar o plano gerado com a CE 70 durante o teste. Depois de *fixar* seu plano preferido, você poderá definir o banco de dados inteiro para usar o nível de compatibilidade e a CE mais recentes. A opção é elaborada a seguir.  
  
### <a name="how-to-force-a-particular-query-plan"></a>Como forçar um plano de consulta específico  
  
O repositório de consultas oferece diferentes maneiras pelas quais você pode forçar o sistema a usar um plano de consulta específico:  
  
- Execute **sp_query_store_force_plan**.  
  
- No [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)], expanda o nó **Repositório de Consultas**, clique com o botão direito do mouse em **Nós que Consomem Mais Recursos** e clique em **Exibir Nós que Consomem Mais Recursos**. A exibição mostra os botões rotulados **Forçar Plano** e **Não Forçar Plano**.  
  
Para obter mais informações sobre o repositório de consultas, veja [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md).  
  
## <a name="examples-of-ce-improvements"></a>Exemplos de melhorias de CE  
  
Esta seção descreve consultas de exemplo que se beneficiam das melhorias implementadas na CE em versões recentes. Essas são as informações básicas que não exigem ação específica de sua parte.  
  
### <a name="example-a-ce-understands-maximum-value-might-be-higher-than-when-statistics-were-last-gathered"></a>Exemplo A. A CE entende que o valor máximo pode ser maior do que quando as estatísticas foram coletadas pela última vez  
  
Suponha que as estatísticas foram coletadas pela última vez para `OrderTable` em `2016-04-30`, quando o `OrderAddedDate` máximo era `2016-04-30`. A CE 120 (e versão superior) entende que as colunas em `OrderTable` que têm dados *crescentes* pode ter valores maiores do que o máximo registrado pelas estatísticas. Esse entendimento melhora o plano de consulta para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] SELECT como a seguinte.  
  
```sql  
SELECT CustomerId, OrderAddedDate  
FROM OrderTable  
WHERE OrderAddedDate >= '2016-05-01';  
```  
  
### <a name="example-b-ce-understands-that-filtered-predicates-on-the-same-table-are-often-correlated"></a>Exemplo B. A CE entende que os predicados filtrados na mesma tabela estão frequentemente correlacionados  
  
Na SELECT a seguir, vemos predicados filtrados em `Model` e em `ModelVariant`. Intuitivamente, entendemos que quando `Model` é 'Xbox' há uma possibilidade de `ModelVariant` ser 'One', uma vez que o Xbox tem uma variante chamada One.  
  
A partir da CE 120, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] entende que pode haver uma correlação entre as duas colunas na mesma tabela, `Model` e `ModelVariant`. A CE faz uma estimativa mais precisa de quantas linhas serão retornadas pela consulta, e o [otimizador de consulta](../../relational-databases/query-processing-architecture-guide.md#optimizing-select-statements) gera um plano melhor.  
  
```sql  
SELECT Model, Purchase_Price  
FROM dbo.Hardware  
WHERE Model = 'Xbox' AND  
      ModelVariant = 'One';  
```  
  
### <a name="example-c-ce-no-longer-assumes-any-correlation-between-filtered-predicates-from-different-tables"></a>Exemplo C. A CE não pressupõe mais nenhuma correlação entre os predicados filtrados de tabelas diferentes 
Com a nova e ampla pesquisa sobre cargas de trabalho modernas e dados corporativos reais, descobriu-se que, em geral, não há correlação entre os filtros de predicado de diferentes tabelas. Na consulta a seguir, a CE pressupõe que não há nenhuma correlação entre `s.type` e `r.date`. Portanto, a CE faz uma estimativa inferior do número de linhas retornadas.  
  
```sql  
SELECT s.ticket, s.customer, r.store  
FROM dbo.Sales AS s  
CROSS JOIN dbo.Returns AS r  
WHERE s.ticket = r.ticket AND  
      s.type = 'toy' AND  
      r.date = '2016-05-11';  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorar e ajustar o desempenho](../../relational-databases/performance/monitor-and-tune-for-performance.md)   
 [Otimizar os planos de consulta com o avaliador de cardinalidade do SQL Server 2014](/previous-versions/dn673537(v=msdn.10))  
 [Dicas de consulta](../../t-sql/queries/hints-transact-sql-query.md)     
 [Dicas de consulta USE HINT](../../t-sql/queries/hints-transact-sql-query.md#use_hint)       
 [Atualizando bancos de dados usando o Assistente de Ajuste de Consulta](../../relational-databases/performance/upgrade-dbcompat-using-qta.md)           
 [Monitorando o desempenho com o repositório de consultas](../../relational-databases/performance/monitoring-performance-by-using-the-query-store.md)    
 [Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)