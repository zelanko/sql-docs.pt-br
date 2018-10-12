---
title: Processamento inteligente de consultas em bancos de dados Microsoft SQL | Microsoft Docs
description: Recursos de processamento inteligente de consulta para melhorar o desempenho da consulta no SQL Server e no Banco de Dados SQL do Azure.
ms.custom: ''
ms.date: 09/24/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: ''
ms.topic: conceptual
helpviewer_keywords: ''
ms.assetid: ''
author: joesackmsft
ms.author: josack
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 35306ebbde5586401f78f368334634f0fadfe7a2
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47753964"
---
# <a name="intelligent-query-processing-in-sql-databases"></a>Processamento inteligente de consultas em bancos de dados SQL
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

A família de recursos **Processamento de consulta inteligente** inclui recursos de amplo impacto que melhoram o desempenho de cargas de trabalho existentes com esforço mínimo de implementação.

![Recursos de processamento de consulta inteligente](./media/2_IQPFeatureFamily.png)

## <a name="adaptive-query-processing"></a>Processamento de consulta adaptável
A família de recursos de processamento de consulta adaptável inclui aprimoramentos do processo de consulta que adaptará estratégias de otimização para as condições de tempo de execução da carga de trabalho do aplicativo. Esses aprimoramentos incluem: uniões adaptáveis do modo de lote, comentários de concessão de memória e execução intercalada para funções com valor de tabela e várias instruções.

### <a name="batch-mode-adaptive-joins"></a>Junções adaptáveis de modo de lote
Esse recurso permite que seu plano mude dinamicamente para uma melhor estratégia de junção durante a execução usando um único plano armazenado em cache.

### <a name="row-and-batch-mode-memory-grant-feedback"></a>Comentários de concessão de memória do modo de lote e linha
> [!NOTE]
> Feedback de concessão de memória do modo de linha é uma versão prévia pública do recurso.  

Esse recurso recalcula a memória real necessária para uma consulta e, em seguida, atualiza o valor de concessão para o plano armazenado em cache, reduzindo concessões de memória excessivas que afetam a simultaneidade e corrigindo concessões de memória subestimadas que causam derramamentos de alto custo para o disco.

### <a name="interleaved-execution-for-multi-statement-table-valued-functions-mstvfs"></a>Execução Intercalada para MSTVFs (funções com valor de tabela de várias instruções)
Com a execução intercalada, as contagens de linha reais da função são usadas para tornar decisões de plano de consulta downstream mais embasadas. 

Para saber mais, confira [Processamento de consultas adaptável em bancos de dados SQL](../../relational-databases/performance/adaptive-query-processing.md).

## <a name="table-variable-deferred-compilation"></a>Compilação adiada de variável da tabela
> [!NOTE]
> A compilação adiada de variável de tabela é uma versão prévia pública do recurso.  

A compilação adiada de variável da tabela melhora a qualidade do plano e o desempenho geral para consultas que fazem referência a variáveis de tabela. Durante a otimização e compilação inicial, esse recurso propagará estimativas de cardinalidade com base nas contagens reais de linha de variável de tabela.  Essas informações de contagem de linha precisas serão ser usadas para otimizar operações de plano de downstream.

Com a compilação adiada de variável de tabela, a compilação de uma instrução que faz referência a uma variável de tabela é adiada até a primeira execução real da instrução. Esse comportamento de compilação adiada é idêntico ao comportamento das tabelas temporárias, e essa alteração resulta no uso de cardinalidade real, em vez do palpite original de uma linha. Para habilitar a versão prévia da compilação adiada de variável de tabela no Banco de Dados SQL do Azure, habilite o nível de compatibilidade do banco de dados 150 para o banco de dados ao qual você está conectado ao executar a consulta.

Para saber mais, veja [Compilação adiada de variável da tabela](../../t-sql/data-types/table-transact-sql.md#table-variable-deferred-compilation ).

## <a name="approximate-query-processing"></a>Processamento de consulta aproximada
> [!NOTE]
> APPROX_COUNT_DISTINCT é um recurso em versão prévia pública.  

O processamento de consulta aproximada é uma nova família de recursos projetados para fornecer agregações em grandes conjuntos de dados, nos quais a capacidade de resposta é mais importante do que a precisão absoluta.  Um exemplo pode ser o cálculo de um COUNT(DISTINCT()) entre 10 bilhões de linhas, para exibição em um painel.  Nesse caso, a precisão absoluto não é importante, mas a capacidade de resposta é essencial. A nova função de agregação APPROX_COUNT_DISTINCT retorna o número aproximado de valores não nulos exclusivos em um grupo.

Para saber mais, confira [APPROX_COUNT_DISTINCT (Transact-SQL)](../../t-sql/functions/approx-count-distinct-transact-sql.md).

## <a name="batch-mode-on-rowstore"></a>Modo de Lote no Rowstore 
> [!NOTE]
> O Modo de Lote no Rowstore é uma versão prévia pública do recurso.  

### <a name="background"></a>Plano de fundo
O SQL Server 2012 introduziu um novo recurso para acelerar as cargas de trabalho analíticas: índices columnstore. Expandimos os casos de uso e melhoramos o desempenho de índices columnstore em todas as versões subsequentes. Até agora, elaboramos e documentamos todas essas funcionalidades como um único recurso: criar os índices columnstore em suas tabelas e sua carga de trabalho analítica “é simplesmente mais rápido”. Nos bastidores, no entanto, há dois conjuntos relacionados, mas distintos, de tecnologias:
- Índices **columnstore** permitem que consultas analíticas acessem apenas os dados nas colunas que precisam. O formato columnstore também possibilita uma compactação muito mais eficiente do que a obtida com a compactação de página em índices “rowstore” tradicionais. 
- O processamento de **modo de lote** permite que os operadores de consulta processem dados com mais eficiência trabalhando em um lote de linhas por vez, em vez de uma linha por vez. Diversos outros aprimoramentos de escalabilidade estão ligados ao processamento do modo de lote.

Os dois conjuntos de recursos funcionam juntos para melhorar a utilização de CPU e E/S:
- Índices columnstore permitem que mais dados caibam na memória e, portanto, reduzem a necessidade de E/S.
- O processamento de modo de lote usa a CPU com mais eficiência.

As duas tecnologias tiram proveito um do outro sempre que possível. Por exemplo, agregações de modo de lote podem ser avaliadas como parte de uma verificação de índice columnstore. Também processamos os dados de columnstore compactados usando a codificação de tamanho de execução com muito mais eficiência com junções de modo de lote e agregações de modo de lote. 
 
Os dois recursos já podem ser usados de forma independente: você pode obter planos do modo de linha que usam índices columnstore e planos de modo de lote que usam somente índices rowstore. Porém, visto que na maioria dos casos os melhores resultados são obtidos quando os dois recursos são usados juntos, o otimizador de consulta do SQL considerou, até o momento, apenas o processamento de modo de lote para consultas que envolvem pelo menos uma tabela com um índice columnstore.

Para alguns aplicativos, os índices columnstore não são uma opção viável porque o aplicativo usa algum outro recurso que não é compatível com índices columnstore (gatilhos não são compatíveis com tabelas com índices columnstore clusterizados, por exemplo). Mais importante, os índices columnstore adicionam sobrecarga às instruções DELETE e UPDATE, pois modificações in-loco não são compatíveis com a compactação columnstore. Para algumas cargas de trabalho transacionais-analíticas híbridas, o benefício que os índices columnstore trariam para as consultas analíticas é superada pela sobrecarga relacionada a um aspecto transacional da carga de trabalho. Esses cenários podem obter a melhor utilização de CPU do processamento em modo de lote sozinho, razão pela qual o recurso **modo de lotes no rowstore** considerará o modo de lote para todas as consultas, independentemente dos índices envolvidos.

### <a name="what-workloads-may-benefit-from-batch-mode-on-rowstore"></a>Quais cargas de trabalho podem se beneficiar com o modo de lote no rowstore
As seguintes cargas de trabalho podem se beneficiar com o modo de lote no rowstore:
1.  Uma parte significativa da carga de trabalho consiste em consultas analíticas (como regra geral, as consultas com operadores, como junções ou agregações processam centenas de milhares de linhas ou mais), **E**
2.  A carga de trabalho é limitada pela CPU (se o gargalo for E/S, ainda é recomendado considerar um índice columnstore, se possível), **E**
3.  Criar um índice columnstore adiciona sobrecarga excessiva à parte transacional da carga de trabalho **OU** criar um índice columnstore não é viável porque seu aplicativo depende de um recurso que ainda não é compatível com índice columnstore.

### <a name="what-changes-with-batch-mode-on-rowstore"></a>O que muda com o modo de lote no rowstore
Além de mover para o nível de compatibilidade 150, não é necessário mudar nada no seu lado para habilitar o modo de lote no rowstore para cargas de trabalho do candidato.

Mesmo se uma consulta não envolver nenhuma tabela com um índice columnstore, o processador de consultas agora usa heurística para decidir se deve considerar o modo de lote. A heurística consiste em:
1.  Uma verificação inicial dos tamanhos de tabela, operadores usados e cardinalidades estimadas na consulta de entrada.
2.  Pontos de verificação adicionais à medida que o otimizador descobre planos novos e mais baratos para a consulta. Se esses planos alternativos não usarem o modo de lote de forma significativa, o otimizador parará de explorar as alternativas de modo de lote.

Se o modo de lote no rowstore for usado, no plano de execução de consulta, você verá o modo de execução real como “modo de lote” usado pelo operador de verificação para heaps no disco e os índices de árvore B.  Essa verificação de modo de lote pode avaliar os filtros de bitmap do modo de lote.  Você também pode ver outros operadores de modo de lote no plano, como junções hash, agregações baseadas em hash, classificações, agregações de janela, filtros, concatenações e operadores escalares de computação.

### <a name="remarks"></a>Remarks
1.  Não há nenhuma garantia de que os planos de consulta usarão o modo de lote. O otimizador de consulta pode decidir se o modo de lote não parecer útil para a consulta. 
2.  Como o espaço de pesquisa do otimizador de consulta está sendo alterado, não há nenhuma garantia de que se você receba um plano de modo de linha, será o mesmo que o plano que você obtém em um nível de compatibilidade inferior. Não há nenhuma garantia de que, se você receber um plano de modo de lote, será o mesmo que o plano que você receberia com um índice columnstore. 
3.  Planos também podem alterar de forma sutil para consultas que combinam os índices columnstore e rowstore, devido à verificação de rowstore de novo modo de lote.
4.  As limitações atuais para o novo modo de lote na verificação do rowstore: ele não será iniciado para tabelas OLTP in-memory ou para qualquer índice diferente de heaps em disco e árvores B. Ele também não será iniciado se uma coluna LOB for buscada ou filtrada. Essa limitação inclui conjuntos de colunas esparsas e colunas XML.
5.  Há consultas para qual o modo de lote não é usado, mesmo com índices columnstore (por exemplo, consultas envolvendo cursores) e essas mesmas exclusões estendem-se também para o modo de lotes no rowstore.

### <a name="configuring-batch-mode-on-rowstore"></a>Configurar o modo de lote no rowstore
A configuração com escopo de banco de dados BATCH_MODE_ON_ROWSTORE é ativada por padrão e pode ser usada para desabilitar o modo de lote no rowstore sem exigir uma alteração no nível de compatibilidade do banco de dados:
```sql
-- Disabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = OFF;

-- Enabling batch mode on rowstore
ALTER DATABASE SCOPED CONFIGURATION SET BATCH_MODE_ON_ROWSTORE = ON;
```
É possível desabilitar o modo de lote no rowstore por meio de configuração com escopo do banco de dados, mas ainda substituir a configuração no nível da consulta usando a dica de consulta ALLOW_BATCH_MODE. O exemplo a seguir habilita o modo de lote no rowstore, mesmo com o recurso desabilitado por meio de configuração com escopo do banco de dados:
```sql
SELECT [Tax Rate], [Lineage Key], [Salesperson Key], SUM(Quantity) AS SUM_QTY, SUM([Unit Price]) AS SUM_BASE_PRICE, COUNT(*) AS COUNT_ORDER
FROM Fact.OrderHistoryExtended
WHERE [Order Date Key]<=DATEADD(dd, -73, '2015-11-13')
GROUP BY [Tax Rate], [Lineage Key], [Salesperson Key]
ORDER BY [Tax Rate], [Lineage Key], [Salesperson Key]
OPTION(RECOMPILE, USE HINT('ALLOW_BATCH_MODE'));
```
Também é possível desabilitar o modo de lote no rowstore para uma consulta específica usando a dica de consulta DISALLOW_BATCH_MODE. Por exemplo:
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
[Referência de operadores físicos e lógicos de plano de execução](../../relational-databases/showplan-logical-and-physical-operators-reference.md)    
[Junções](../../relational-databases/performance/joins.md)    
[Demonstrar o processamento de consulta adaptável](https://github.com/joesackmsft/Conferences/blob/master/Data_AMP_Detroit_2017/Demos/AQP_Demo_ReadMe.md)       
[Demonstrar QP inteligente](https://github.com/joesackmsft/Conferences/blob/master/IQPDemos/IQP_Demo_ReadMe.md)   
