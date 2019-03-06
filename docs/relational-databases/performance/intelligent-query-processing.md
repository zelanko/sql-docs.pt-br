---
title: Processamento inteligente de consultas em bancos de dados Microsoft SQL | Microsoft Docs
description: Recursos de processamento inteligente de consulta para melhorar o desempenho da consulta no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 02/21/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 1b92bc15079fcc85212ea3d1b51be64a3348a4b1
ms.sourcegitcommit: 2663063e29f2868ee6b6d596df4b2af2d22ade6f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/04/2019
ms.locfileid: "57305364"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Processamento inteligente de consultas em bancos de dados SQL

[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A família de recursos de processamento de consulta (QP) inteligente inclui recursos de impacto abrangente. Eles melhoram o desempenho de cargas de trabalho existentes com um esforço mínimo de implementação. Para se beneficiar automaticamente dessa família de recursos, mude para o nível de compatibilidade aplicável do banco de dados.

| **Recurso IQP** | **Com suporte no Banco de Dados SQL do Azure** | **Com suporte no SQL Server** |
| --- | --- | --- |
| [Junções adaptáveis (Modo de Lote)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-adaptive-joins) | Sim, no nível de compatibilidade 140| Sim, a partir do SQL Server 2017 no nível de compatibilidade 140|
| [Distinção de contagem aproximada](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#approximate-query-processing) | Sim, versão prévia pública| Sim, a partir do SQL Server de 2019 CTP 2.0, versão prévia pública|
| [Modo de Lote no Rowstore](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#batch-mode-on-rowstore) | Sim, no nível de compatibilidade 150, versão prévia pública| Sim, a partir do SQL Server 2019 CTP 2.0 no nível de compatibilidade 150, versão prévia pública|
| [Execução intercalada](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#interleaved-execution-for-multi-statement-table-valued-functions) | Sim, no nível de compatibilidade 140| Sim, a partir do SQL Server 2017 no nível de compatibilidade 140|
| [Comentários de concessão de memória (Modo de Lote)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#batch-mode-memory-grant-feedback) | Sim, no nível de compatibilidade 140| Sim, a partir do SQL Server 2017 no nível de compatibilidade 140|
| [Comentários de concessão de memória (Modo de Lote)](https://docs.microsoft.com/en-us/sql/relational-databases/performance/adaptive-query-processing?view=sql-server-2017#row-mode-memory-grant-feedback) | Sim, no nível de compatibilidade 150, versão prévia pública| Sim, a partir do SQL Server 2019 CTP 2.0 no nível de compatibilidade 150, versão prévia pública|
| [Inlining de UDF escalar](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#scalar-udf-inlining) | Não, mas está planejado para uma atualização futura | Sim, a partir do SQL Server 2019 CTP 2.1 no nível de compatibilidade 150, versão prévia pública|
| [Compilação Adiada de Variável da Tabela](https://docs.microsoft.com/en-us/sql/relational-databases/performance/intelligent-query-processing?view=sql-server-2017#table-variable-deferred-compilation) | Sim, no nível de compatibilidade 150, versão prévia pública| Sim, a partir do SQL Server 2019 CTP 2.0 no nível de compatibilidade 150, versão prévia pública|



## <a name="adaptive-query-processing"></a>Processamento de consulta adaptável

A família de recursos de processamento de consulta adaptável inclui as seguintes melhorias de processamento de consulta. Essas melhorias adaptarão estratégias de otimização para as condições de tempo de execução da sua carga de trabalho do aplicativo: 
- Junções adaptáveis de modo de lote
- Comentários de concessão de memória
- Execução Intercalada para MSTVFs (funções com valor de tabela de várias instruções)

### <a name="batch-mode-adaptive-joins"></a>Junções adaptáveis de modo de lote

Com esse recurso, seu plano pode mudar dinamicamente para melhorar a estratégia de junção durante a execução ao usar um único plano armazenado em cache.

Para obter mais informações sobre uniões adaptáveis do modo de lote, confira [Processamento de consulta adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentários de concessão de memória do modo de lote e linha

> [!NOTE]
> Feedback de concessão de memória do modo de linha é uma versão prévia pública do recurso.  

Esse recurso recalcula a memória real necessária para uma consulta. Em seguida, ele atualiza o valor de concessão no plano de cache. Isso reduz as concessões excessivas de memória que afetam a simultaneidade. Esse recurso também corrige concessões subestimadas de memória que causam despejos dispendiosos no disco.

Para saber mais sobre comentários de concessão de memória, confira [Processamento de consultas adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

### <a name="interleaved-execution-for-mstvfs"></a>Execução intercalada para MSTVFs

Com a execução intercalada, as contagens de linha reais da função são usadas para tornar decisões de plano de consulta downstream mais embasadas. Confira mais informações sobre MSTVFs (funções com valor de tabela de várias instruções) em [Funções com Valor de Tabela](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#TVF).

Para obter mais informações sobre a execução intercalada, confira [Processamento de consulta adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilação adiada de variável da tabela

> [!NOTE]
> A compilação adiada de variável de tabela é uma versão prévia pública do recurso.  

A compilação adiada de variável da tabela melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propaga estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela. Essas informações de contagem de linha precisas otimizam as operações de plano de downstream.

A compilação adiada de variável de tabela adia a compilação de uma instrução que faz referência a uma variável de tabela até a primeira execução real da instrução. Esse comportamento de compilação adiada é igual ao das tabelas temporárias. Essa alteração resulta no uso de cardinalidade real em vez da estimativa original de uma linha. 

Você pode ativar a versão prévia pública da compilação adiada de variável de tabela no Banco de Dados SQL do Azure. Para isso, habilite o nível de compatibilidade 150 do banco de dados ao qual você está conectado ao executar a consulta.

Para saber mais, veja [Compilação adiada de variável da tabela](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation).

## <a name="scalar-udf-inlining"></a>Embutimento de UDF escalar

> [!NOTE]
> O inlining de UDF (função definida pelo usuário) escalar é a versão prévia pública do recurso.  

O inlining da UDF escalar transforma automaticamente [UDFs escalares](../../relational-databases/user-defined-functions/create-user-defined-functions-database-engine.md#Scalar) em expressões relacionais. Ele as incorpora à chamada da consulta SQL. Essa transformação melhora o desempenho de cargas de trabalho que aproveitam as UDFs escalares. O inlining da UDF escalar facilita a otimização baseada em custo de operações das UDFs. Os resultados são eficientes, orientados para conjunto e paralelos, em vez de planos de execução ineficientes, iterativos e seriais. Esse recurso é habilitado por padrão no nível de compatibilidade do banco de dados 150.

Para saber mais, confira [Scalar UDF Inlining](../user-defined-functions/scalar-udf-inlining.md) (Embutimento de UDF escalar).

## <a name="approximate-query-processing"></a>Processamento de consulta aproximada

> [!NOTE]
> **APPROX_COUNT_DISTINCT** é uma versão prévia pública do recurso.  

O processamento de consulta aproximado é uma nova família de recursos. Ele agrega grandes conjuntos de dados nos quais a capacidade de resposta é mais importante do que a precisão absoluta. Um exemplo é o cálculo de **COUNT(DISTINCT())** entre 10 bilhões de linhas para a exibição em um painel. Nesse caso, o que é importante não é a precisão absoluta, mas a capacidade de resposta que é essencial. A nova função de agregação **APPROX_COUNT_DISTINCT** retorna o número aproximado de valores não nulos exclusivos em um grupo.

Para saber mais, confira [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modo de Lote no Rowstore 

> [!NOTE]
> O modo de lote no Rowstore é uma versão prévia pública do recurso.  

O modo de lote em rowstore permite que a execução em modo de lote para cargas de trabalho analíticas sem a necessidade de índices columnstore.  Esse recurso dá suporte a filtros de bitmap e à execução do modo de lote para em disco heaps e índices de árvore B. O modo de lote em rowstore habilita o suporte para todos os operadores habilitados para o modo de lote existente.

### <a name="background"></a>Plano de fundo

[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] introduziu um novo recurso para acelerar as cargas de trabalho analíticas: os índices columnstore. Expandimos os casos de uso e melhoramos o desempenho de índices columnstore em todas as versões subsequentes. Até agora, apresentamos e documentamos todos esses recursos como um único recurso. Você pode criar índices columnstore em suas tabelas. E sua carga de trabalho analítica será bem mais rápida. No entanto, há dois conjuntos de tecnologias relacionados mas distintos:
- Com os índices **columnstore**, as consultas analíticas acessam apenas os dados que elas precisam das colunas. A compactação de página no formato columnstore também é mais eficiente do que a dos índices **rowstore** tradicionais. 
- Com o processamento em **modo de lote**, os operadores de consulta processam dados com mais eficiência. Eles funcionam em um lote de linhas em vez de uma linha por vez. Diversos outros aprimoramentos de escalabilidade estão ligados ao processamento do modo de lote. Confira mais informações sobre o modo de lote em [Modos de execução](../../relational-databases/query-processing-architecture-guide.md#execution-modes).

Os dois conjuntos de recursos funcionam juntos para melhorar a utilização de CPU e E/S (entrada/saída):
- ao usar índices columnstore, mais dos seus dados se encaixam na memória. Isso reduz a necessidade de E/S.
- O processamento de modo de lote usa a CPU com mais eficiência.

As duas tecnologias tiram proveito um do outro sempre que possível. Por exemplo, agregações de modo de lote podem ser avaliadas como parte de uma verificação de índice columnstore. Também processamos os dados de columnstore compactados usando a codificação de tamanho de execução com muito mais eficiência com junções e agregações de modos de lotes. 
 
Os dois recursos podem ser utilizados de forma independente:
* Você obtém planos de modo de linha que usam índices columnstore.
* Você obtém planos de modo de linha que usam somente índices rowstore. 

Geralmente é possível obter os melhores resultados ao usar os dois recursos juntos. Portanto, até agora, o otimizador de consulta do SQL Server considerou o processamento de modo de lote só para consultas que envolvem pelo menos uma tabela com um índice columnstore.

Os índices columnstore não são uma boa opção para alguns aplicativos. Pode ser que o aplicativo use outro recurso que não tenha suporte com índices columnstore. Por exemplo, as modificações no local não são compatíveis com a compactação de columnstore. Portanto, os gatilhos não têm suporte em tabelas com índices columnstore clusterizados. E mais importante, índices columnstore adicionam uma sobrecarga para as instruções **DELETE** e **UPDATE**. 

Para algumas cargas de trabalho transacionais analíticas híbridas, a sobrecarga relacionada a aspectos transacionais da carga de trabalho superam os benefícios dos índices columnstore. Tais cenários podem melhorar o uso de CPU do processamento de modo de lote. É por isso que o modo de lote no recurso de rowstore considera o modo de lote para todas as consultas. Não importa quais índices estão envolvidos.

### <a name="workloads-that-might-benefit-from-batch-mode-on-rowstore"></a>Cargas de trabalho que podem se beneficiar com o modo de lote no rowstore

As seguintes cargas de trabalho podem se beneficiar do modo de lote no rowstore:
* Uma parte significativa da carga de trabalho consiste em consultas analíticas. Geralmente essas consultas têm operadores como junções ou agregações que processam centenas de milhares de linhas ou mais.
* A carga de trabalho está associada à CPU. Se o gargalo for em E/S, ainda assim é recomendável que você considere um índice columnstore, se possível.
* Criar um índice columnstore adiciona muita sobrecarga à parte transacional da carga de trabalho. Ou a criação de um índice columnstore não é viável porque seu aplicativo depende de um recurso que ainda não tem suporte com índices columnstore.

> [!NOTE]
> O modo de lote em rowstore só pode ajudar a reduzir o consumo de CPU. Se o gargalo for relacionado à E/S e os dados ainda não estiverem armazenados em cache (cache "frio"), o modo de lote em rowstore não melhorará o tempo decorrido. Da mesma forma, se não houver memória suficiente no computador para armazenar em cache todos os dados, será improvável que ocorra uma melhoria de desempenho.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>O que muda com o modo de lote no rowstore?

Além de mover para o nível de compatibilidade 150, não é necessário mudar nada no seu lado para habilitar o modo de lote no rowstore para cargas de trabalho candidatas.

Mesmo se uma consulta não envolver nenhuma tabela com um índice columnstore, o processador de consultas já usa heurística para decidir se deve considerar o modo de lote. A heurística consiste destas verificações:
1. Uma verificação inicial dos tamanhos de tabela, operadores usados e cardinalidades estimadas na consulta de entrada.
2. Pontos de verificação adicionais à medida que o otimizador descobre planos novos e mais baratos para a consulta. Se esses planos alternativos não usarem o modo de lote de forma significativa, o otimizador parará de explorar as alternativas de modo de lote.

Se o modo de lote em rowstore for usado, você verá o modo de execução real como o **modo de lote** no plano de consulta. O operador de verificação usa o modo de lote em heaps em discos e índices de árvore B. Essa verificação do modo de lote pode avaliar os filtros de bitmap do modo de lote. Você também poderá ver outros operadores de modo de lote no plano. Os exemplos são junções hash, agregações baseadas em hash, classificações, agregações de janela, filtros, concatenações e operadores escalares de computação.

### <a name="remarks"></a>Remarks

* Planos de consulta nem sempre usam o modo de lote. O otimizador de consulta pode decidir que o modo de lote não é útil para a consulta. 
* O espaço de pesquisa do otimizador de consulta está sendo alterado. Portanto, se você receber um plano de modo de linha, poderia não ser o mesmo que o plano que você obtém em um nível de compatibilidade mais baixo. E se você receber um plano de modo de lote, poderia não ser o mesmo que o plano que você obtém com um índice columnstore. 
* Os planos também podem alterar as consultas que combinam os índices columnstore e rowstore devido à verificação de rowstore do novo modo de lote.
* Existem limitações atuais para o novo modo de lote na verificação de rowstore: 
    * Ele não será iniciado para tabelas OLTP na memória nem para índices diferentes de heaps em disco e árvores B. 
    * Ele também não será iniciado ao buscar ou filtrar uma coluna LOB (de objeto grande). Essa limitação inclui conjuntos de colunas esparsas e colunas XML.
* Há consultas em que o modo de lote não é usado para pares em índices columnstore. Os exemplos são consultas que envolvem cursores. Essas mesmas exclusões também se estendem ao modo de lote em rowstore.

### <a name="configure-batch-mode-on-rowstore"></a>Configurar o modo de lote no rowstore

A configuração no escopo do banco de dados **BATCH_MODE_ON_ROWSTORE** é ativada por padrão. Ela desabilita o modo de lote em rowstore sem exigir uma alteração no nível de compatibilidade do banco de dados:

```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```

você pode desabilitar o modo de lote em rowstore por meio de configuração do escopo do banco de dados. Mas você ainda pode substituir a configuração no nível da consulta usando a dica de consulta **ALLOW_BATCH_MODE**. O exemplo a seguir habilita o modo de lote no rowstore, mesmo com o recurso desabilitado por meio de configuração com escopo do banco de dados:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```

Também é possível desabilitar o modo de lote em rowstore para uma consulta específica usando a dica de consulta **DISALLOW_BATCH_MODE**. Consulte o seguinte exemplo:

```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('DISALLOW_BATCH_MODE'));
```

## <a name="see-also"></a>Confira também

[Central de desempenho do Mecanismo de Banco de Dados do SQL Server e do Banco de Dados SQL do Azure](../../relational-databases/performance/performance-center-for-sql-server-database-engine-and-azure-sql-database.md)     
[Guia de arquitetura de processamento de consultas](../../relational-databases/query-processing-architecture-guide.md)    
[Referência de operadores físicos e lógicos do plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)    
[Demonstrar o processamento de consulta adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[Demonstrar QP inteligente](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
