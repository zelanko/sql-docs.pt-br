---
title: Estatísticas
description: O otimizador de consulta usa estatísticas para criar planos de consulta que melhoram o desempenho das consultas. Saiba mais sobre os conceitos e as diretrizes de uso da otimização de consulta.
ms.custom: ''
ms.date: 06/03/2020
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- statistical information [SQL Server], query optimization
- query performance [SQL Server], statistics
- query optimization statistics [SQL Server]
- statistical information [SQL Server], database options
- query optimization statistics [SQL Server], about query optimization statistics
- statistical information [SQL Server], guidelines
- statistical information [SQL Server]
- using statistics [SQL Server]
- statistical information [SQL Server], indexes
- index statistics [SQL Server]
- query optimizer [SQL Server], statistics
- statistics [SQL Server]
ms.assetid: b86a88ba-4f7c-4e19-9fbd-2f8bcd3be14a
author: julieMSFT
ms.author: jrasnick
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dc2c5467768aa92badb1a74e90a9f940eb0732e3
ms.sourcegitcommit: 04cf7905fa32e0a9a44575a6f9641d9a2e5ac0f8
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/07/2020
ms.locfileid: "91810520"
---
# <a name="statistics"></a>Estatísticas

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]
  O otimizador de consulta usa estatísticas para criar planos de consulta que melhoram o desempenho das consultas. Para a maioria das consultas, o otimizador de consulta já gera as estatísticas necessárias para um plano de consulta de alta qualidade. Em alguns casos, é necessário criar estatísticas adicionais ou modificar o design da consulta para obter melhores resultados. Este tópico aborda os conceitos de estatísticas e fornece diretrizes para o uso eficiente de estatísticas de otimização de consultas.  
  
##  <a name="components-and-concepts"></a><a name="DefinitionQOStatistics"></a> Componentes e conceitos  
### <a name="statistics"></a>Estatísticas  
 As estatísticas de otimização de consulta são BLOBs (objetos binários grandes) que contêm informações estatísticas sobre a distribuição de valores em uma ou mais colunas de uma tabela ou exibição indexada. O otimizador de consulta usa essas estatísticas para estimar a *cardinalidade* ou o número de linhas no resultado de consulta. Essas *estimativas de cardinalidade* permitem ao otimizador de consulta criar um plano de consulta de alta qualidade. Por exemplo, dependendo dos predicados, o Otimizador de Consulta pode usar estimativas de cardinalidade para escolher o operador Index Seek em vez de o operador Index Scan, que utiliza mais recursos, melhorando com isso o desempenho das consultas.  
  
 Cada objeto de estatísticas é criado em uma lista de uma ou mais colunas de tabela e inclui um *histograma* que exibe a distribuição de valores na primeira coluna. Os objetos de estatísticas em várias colunas também armazenam informações estatísticas sobre a correlação de valores entre as colunas. Essas estatísticas de correlação, ou *densidades*, são derivadas do número de linhas distintas de valores de coluna. 

#### <a name="histogram"></a><a name="histogram"></a> Histograma  
Um **histograma** mede a frequência de ocorrência de cada valor distinto em um conjunto de dados. O otimizador de consulta calcula um histograma com base nos valores de coluna na primeira coluna de chave do objeto de estatísticas, selecionando os valores de coluna por amostragem estatística das linhas ou pela execução de uma verificação completa de todas as linhas na tabela ou na exibição. Se o histograma for criado com base em um conjunto amostrado de linhas, os totais armazenados para o número de linhas e o número de valores distintos são estimativas e não precisam ser números inteiros.

> [!NOTE]
> <a name="frequency"></a> Os histogramas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são criados apenas para uma única coluna, ou seja, a primeira coluna do conjunto de colunas de chave do objeto de estatísticas.
  
Para criar o histograma, o otimizador de consulta classifica os valores de colunas, calcula o número de valores que correspondem a cada valor de coluna distinta e agrega os valores de colunas em um máximo de 200 etapas de histograma contíguas. Cada etapa do histograma inclui uma gama de valores de coluna seguidos por um valor de coluna de limite superior. O intervalo inclui todos os possíveis valores de coluna entre valores de limite, excluindo-se os próprios valores de limite em si. O mais baixo dos valores de coluna classificados é o valor do limite superior da primeira etapa do histograma.

Mais detalhadamente, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cria o **histograma** com base no conjunto classificado de valores de coluna em três etapas:

- **Inicialização do histograma**: na primeira etapa, uma sequência de valores que começa no início do conjunto classificado é processada e até 200 valores de *range_high_key*, *equal_rows*, *range_rows* e *distinct_range_rows* são coletados (*range_rows* e *distinct_range_rows* são sempre zero durante essa etapa). A primeira etapa termina quando toda a entrada foi esgotada ou quando 200 valores foram encontrados. 
- **Examinar com a mesclagem de bucket**: cada valor adicional da coluna inicial da chave de estatísticas é processado na segunda etapa, na ordem classificada; cada valor sucessivo é adicionado ao último intervalo ou um novo intervalo no final é criado (isso é possível porque os valores de entrada são classificados). Se um novo intervalo for criado, um par dos intervalos vizinhos existentes será recolhido em um único intervalo. Esse par de intervalos é selecionado para minimizar a perda de informações. Esse método usa um algoritmo de *diferença máxima* para minimizar o número de etapas no histograma enquanto maximiza a diferença entre os valores de limite. O número de etapas após o recolhimento dos intervalos permanece em 200 durante toda esta etapa.
- **Consolidação do histograma**: na terceira etapa, mais intervalos podem ser recolhidos se uma quantidade significativa de informações não é perdida. O número de etapas do histograma pode ser menor do que o número de valores distintos, até mesmo para colunas com menos de 200 pontos de limite. Portanto, mesmo se a coluna tiver mais de 200 valores exclusivos, o histograma poderá ter menos de 200 etapas. Para uma coluna que consiste apenas em valores exclusivos, o histograma consolidado terá um mínimo de três etapas.

> [!NOTE]
> Se o histograma foi criado com uma amostra em vez de com a opção fullscan, os valores de *equal_rows*, *range_rows*, *distinct_range_rows* e *average_range_rows* são estimados e, portanto, não precisam ser inteiros.

O diagrama a seguir mostra um histograma com seis etapas: A área à esquerda do primeiro valor do limite superior corresponde à primeira etapa.
  
![Histograma](../../relational-databases/system-dynamic-management-views/media/histogram-2.svg "Histograma") 
  
Para cada etapa do histograma acima:
-   A linha em negrito representa o valor do limite superior (*range_high_key*) e o número de vezes que ele ocorre (*equal_rows*)  
  
-   A área sólida à esquerda de *range_high_key* representa o intervalo de valores de coluna e o número médio de vezes que cada valor de coluna ocorre (*average_range_rows*). As *average_range_rows* da primeira etapa do histograma são sempre 0.  
  
-   As linhas pontilhadas representam os valores amostrados usados para estimar o número total de valores distintos no intervalo (*distinct_range_rows*) e o número total de valores no intervalo (*range_rows*). O otimizador de consulta usa *range_rows* e *distinct_range_rows* para calcular *average_range_rows* e não armazena os valores amostrados.   
  
#### <a name="density-vector"></a><a name="density"></a>Vetor de densidade  
**Densidade** são informações sobre o número de duplicatas em determinada coluna ou em uma combinação de colunas e ele é calculada como 1/(número de valores distintos). O otimizador de consulta usa densidades para aprimorar as estimativas de cardinalidade de consultas que retornam várias colunas da mesma tabela ou exibição indexada. Conforme a densidade diminui, aumenta a seletividade de um valor. Por exemplo, em uma tabela que representa carros, muitos carros têm o mesmo fabricante, mas cada carro tem um VIN (número de identificação de veículo) exclusivo. Um índice no VIN é mais seletivo que um índice no fabricante, porque o VIN tem densidade menor que o fabricante. 

> [!NOTE]
> Frequência são informações sobre a ocorrência de cada valor distinto na primeira coluna de chave do objeto de estatísticas e é calculada como a contagem de linhas * densidade. Uma frequência máxima igual a 1 pode ser encontrada em colunas com valores exclusivos.

O vetor de densidade contém uma densidade para cada prefixo de colunas no objeto de estatísticas. Por exemplo, se um objeto de estatísticas tiver as colunas de chave `CustomerId`, `ItemId` e `Price`, a densidade será calculada em cada um dos prefixos de coluna a seguir.
  
|Prefixo de coluna|Densidade calculada em|  
|---|---|
|(CustomerId)|Linhas com valores correspondentes para CustomerId.|  
|(CustomerId, ItemId)|Linhas com valores correspondentes para CustomerId e ItemId|  
|(CustomerId, ItemId, Price)|Linhas com valores correspondentes para CustomerId, ItemId e Price| 

### <a name="filtered-statistics"></a>Estatísticas filtradas  
 As estatísticas filtradas podem melhorar o desempenho de consultas selecionadas em subconjuntos bem definidos de dados. As estatísticas filtradas usam um predicado do filtro para selecionar o subconjunto de dados incluído nas estatísticas. Estatísticas filtradas bem projetadas podem aprimorar o plano de execução de consultas em comparação com as estatísticas de tabela completa. Para obter mais informações sobre o predicado de filtro, veja [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md). Para obter mais informações sobre quando criar estatísticas filtradas, consulte a seção [Quando criar estatísticas](#CreateStatistics) neste tópico.  
 
### <a name="statistics-options"></a>Opções de estatísticas  
 Há três opções que você pode definir que afetam quando e como as estatísticas são criadas e atualizadas. Estas opções são definidas no nível do banco de dados somente.  
  
#### <a name="auto_create_statistics-option"></a><a name="AutoUpdateStats"></a>Opção AUTO_CREATE_STATISTICS  
 Quando a opção de criação automática de estatísticas, [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics), está ativada, o otimizador de consulta cria estatísticas em colunas individuais no predicado da consulta, conforme necessário, a fim de melhorar as estimativas de cardinalidade do plano de consulta. Essas estatísticas de coluna única são criadas em colunas que ainda não têm um [histograma](#histogram) em um objeto de estatísticas existente. A opção AUTO_CREATE_STATISTICS não determina se são criadas estatísticas para índices. Essa opção também não gera estatísticas filtradas. Ela se aplica estritamente a estatísticas de coluna única para a tabela completa.  
  
 Quando o otimizador de consulta cria estatísticas como resultado do uso da opção AUTO_CREATE_STATISTICS, os nomes das estatísticas começam com `_WA`. Você pode usar a consulta a seguir para determinar se o otimizador de consulta criou estatísticas para uma coluna de predicado de consulta.  
  
```sql  
SELECT OBJECT_NAME(s.object_id) AS object_name,  
    COL_NAME(sc.object_id, sc.column_id) AS column_name,  
    s.name AS statistics_name  
FROM sys.stats AS s 
INNER JOIN sys.stats_columns AS sc  
    ON s.stats_id = sc.stats_id AND s.object_id = sc.object_id  
WHERE s.name like '_WA%'  
ORDER BY s.name;  
```  
  
#### <a name="auto_update_statistics-option"></a>Opção AUTO_UPDATE_STATISTICS  
 Quando a opção de atualização automática de estatísticas, [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics), está ativada, o otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando são usadas por uma consulta. As estatísticas ficam desatualizadas depois que operações de inserção, atualização, exclusão ou mesclagem alteram a distribuição de dados na tabela ou na exibição indexada. O otimizador de consulta determina quando estatísticas podem estar desatualizadas contando o número de modificações de dados desde a última atualização das estatísticas e comparando o número de modificações a um limite. O limite se baseia no número de linhas na tabela ou na exibição indexada.  
  
* Até o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um limite com base na porcentagem de linhas alteradas. Isso ocorre independentemente do número de linhas na tabela. O limite é:
    * Se a cardinalidade da tabela era de 500 ou menos quando as estatísticas foram avaliadas, é necessário atualizar a cada 500 modificações.
    * Se a cardinalidade da tabela era inferior a 500 quando as estatísticas foram avaliadas, é necessário atualizar a cada 500 + 20% de modificações.

* Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [nível de compatibilidade de banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 130, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa um limite de atualização de estatística dinâmico e decrescente, ajustado de acordo com o número de linhas da tabela. Isso é calculado como a raiz quadrada do produto de 1000 e da cardinalidade da tabela atual. Por exemplo, se a tabela contiver 2 milhões de linhas, o cálculo será sqrt(1000 * 2000000) = 44721,359. Com essa alteração, as estatísticas em tabelas grandes serão atualizadas com mais frequência. No entanto, quando um banco de dados tem um nível de compatibilidade inferior a 130, aplica-se o limite do [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]. ?

> [!IMPORTANT]
> Do [!INCLUDE[ssKilimanjaro](../../includes/ssKilimanjaro-md.md)] até o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] ou no [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e versões posteriores, em [nível de compatibilidade do banco de dados](../../relational-databases/databases/view-or-change-the-compatibility-level-of-a-database.md) 120 e inferior, habilite o [sinalizador de rastreamento 2371](../../t-sql/database-console-commands/dbcc-traceon-trace-flags-transact-sql.md) para que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] use um limite de atualização de estatísticas dinâmico e decrescente.

Você pode usar as seguintes diretrizes para habilitar o sinalizador de rastreamento 2371 em seu ambiente pré-[!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]:

 - Se você não observar problemas de desempenho devido a estatísticas desatualizadas, não será necessário habilitar esse sinalizador de rastreamento.
 - Se você estiver em sistemas SAP, habilite o sinalizador de rastreamento.  Confira mais informações neste [blog](/archive/blogs/saponsqlserver/changes-to-automatic-update-statistics-in-sql-server-traceflag-2371).
 - Se for necessário contar com o trabalho noturno para atualizar estatísticas porque a atualização automática atual não é disparada com uma frequência suficiente, considere habilitar o sinalizador de rastreamento 2371 para reduzir o limite.
  
O otimizador de consulta procura estatísticas desatualizadas antes de compilar uma consulta e antes de executar um plano de consulta em cache. Antes de compilar uma consulta, o otimizador usa as colunas, tabelas e exibições indexadas no predicado de consulta para determinar quais estatísticas podem estar desatualizadas. Antes de executar um plano de consulta em cache, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] verifica se o plano de consulta faz referência a estatísticas atualizadas.  
  
A opção AUTO_UPDATE_STATISTICS se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) . Essa opção também se aplica a estatísticas filtradas.  
 
Você pode usar [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) para controlar com precisão o número de linhas alteradas em uma tabela e decidir se deseja atualizar manualmente as estatísticas.



  
#### <a name="auto_update_statistics_async"></a>AUTO_UPDATE_STATISTICS_ASYNC  
 A opção de atualização de estatísticas assíncrona, [AUTO_UPDATE_STATISTICS_ASYNC](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics_async), determina se o otimizador de consulta usa atualizações de estatísticas síncronas ou assíncronas. Por padrão, a opção de atualização de estatísticas assíncrona está desativada e o otimizador de consulta atualiza estatísticas de forma síncrona. A opção AUTO_UPDATE_STATISTICS_ASYNC se aplica a objetos de estatísticas criados para índices, colunas únicas em predicados de consulta e estatísticas criadas com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) .  
 
 > [!NOTE]
 > Para definir a opção de atualização de estatísticas assíncrona no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], na página *Opções* da janela *Propriedades do Banco de Dados*, as opções *Atualizar Estatísticas Automaticamente* e *Atualizar Estatísticas Automaticamente de Forma Assíncrona* devem ser definidas como **Verdadeiro**.
  
 As atualizações de estatísticas podem ser síncronas (o padrão) ou assíncronas. Com as atualizações de estatísticas síncronas, as consultas são sempre compiladas e executadas com estatísticas atualizadas. Quando as estatísticas estão desatualizadas, o otimizador de consulta aguarda estatísticas atualizadas antes de compilar e executar a consulta. Com as atualizações de estatísticas assíncronas, as consultas são compiladas com estatísticas existentes, mesmo que elas estejam desatualizas. O otimizador de consulta poderá escolher um plano de consulta com qualidade inferior se as estatísticas estiverem desatualizadas na compilação da consulta. As consultas compiladas após a conclusão das atualizações assíncronas serão beneficiadas por usarem estatísticas atualizadas.  
  
 Considere o uso de estatísticas síncronas ao executar operações que alteram a distribuição de dados, como truncar uma tabela ou executar uma atualização em massa de uma porcentagem grande das linhas. Se você não atualizar as estatísticas depois de concluir a operação, o uso de estatísticas síncronas garantirá que as estatísticas sejam atualizadas antes de executar consultas nos dados alterados.  
  
 Considere o uso de estatísticas assíncronas para obter tempos de resposta de consulta mais previsíveis para os seguintes cenários:  
  
* Seu aplicativo executa frequentemente a mesma consulta, consultas semelhantes ou planos de consulta em cache semelhantes. Os tempos de resposta de consulta podem ser mais previsíveis com atualizações de estatísticas assíncronas do que com atualizações de estatísticas síncronas, pois o otimizador de consulta pode executar consultas de entrada sem aguardar estatísticas atualizadas. Isso evita o atraso de algumas consultas e não de outras.  
  
* Seu aplicativo excedeu o tempo limite de solicitações do cliente pelo fato de uma ou mais consultas estarem aguardando a atualização de estatísticas. Em alguns casos, a espera por estatísticas síncronas pode gerar falhas em aplicativos com tempo limite restrito.  

A atualização de estatísticas assíncronas é executada por uma solicitação em segundo plano. Quando a solicitação estiver pronta para gravar estatísticas atualizadas no banco de dados, ela tentará adquirir um bloqueio de modificação de esquema no objeto de metadados de estatísticas. Caso uma sessão diferente já esteja mantendo um bloqueio no mesmo objeto, a atualização de estatísticas assíncronas será bloqueada até que o bloqueio de modificação do esquema possa ser adquirido. Da mesma forma, as sessões que precisam adquirir um bloqueio de estabilidade do esquema no objeto de metadados de estatísticas para compilar uma consulta poderão ser bloqueadas pela sessão em segundo plano da atualização de estatísticas assíncronas, pois ela já está aguardando para adquirir o bloqueio de modificação do esquema. Portanto, para cargas de trabalho com compilações de consulta muito frequentes e atualizações de estatísticas frequentes, usar estatísticas assíncronas poderá aumentar a probabilidade de ocorrer problemas de simultaneidade devido ao bloqueio.

No Banco de Dados SQL do Azure você pode evitar possíveis problemas de simultaneidade usando a atualização de estatísticas assíncronas caso habilite a [configuração no escopo do banco de dados](../../t-sql/statements/alter-database-scoped-configuration-transact-sql.md) ASYNC_STATS_UPDATE_WAIT_AT_LOW_PRIORITY. Com essa configuração habilitada, a solicitação em segundo plano aguardará para adquirir o bloqueio de modificação do esquema em uma fila de baixa prioridade separada, permitindo que outras solicitações continuem compilando consultas com as estatísticas existentes. Quando nenhuma outra sessão estiver mantendo um bloqueio no objeto de metadados de estatísticas, a solicitação em segundo plano adquirirá um bloqueio de modificação de esquema e uma atualização de estatísticas. Na hipótese improvável em que a solicitação em segundo plano não possa adquirir o bloqueio dentro de um período de tempo limite de vários minutos, a atualização de estatísticas assíncronas será anulada e as estatísticas não serão atualizadas até que outra atualização de estatísticas automática seja disparada ou até que as estatísticas sejam [atualizadas manualmente](update-statistics.md).

#### <a name="incremental"></a>INCREMENTAL  
 Quando a opção INCREMENTAL de CREATE STATISTICS for ON, as estatísticas serão criadas de acordo com as estatísticas da partição. Quando estiver OFF, a árvore de estatísticas será ignorada e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] recomputará as estatísticas. O padrão é OFF. Essa configuração substitui a propriedade INCREMENTAL de nível de banco de dados. Para obter informações sobre como criar estatísticas incrementais, consulte [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md). Para obter mais informações sobre como criar estatísticas por partição automaticamente, consulte [Propriedades de banco de dados &#40;página Opções&#41;](../../relational-databases/databases/database-properties-options-page.md#automatic) e [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md). 
  
 Quando as novas partições são adicionados a uma tabela grande, as estatísticas devem ser atualizadas para incluir as novas partições. No entanto, o tempo necessário para digitalizar a tabela inteira (opção FULLSCAN ou SAMPLE) podem ser muito longos. Além disso, digitalizar a tabela inteira não é necessário porque somente as estatísticas nas novas partições podem ser necessárias. A opção incremental cria e armazena estatísticas por partição e, quando atualizada, somente atualiza estatísticas nessas partições que precisam de novas estatísticas  
  
 Se as estatísticas por partição não tiverem suporte, a opção será ignorada e um aviso será gerado. As estatísticas incrementais não têm suporte para os seguintes tipos de estatísticas:  
  
* Estatísticas criadas com os índices que não estejam alinhados por partição com a tabela base.  
* Estatísticas criadas em bancos de dados secundários legíveis AlwaysOn.  
* Estatísticas criadas em bancos de dados somente leitura.  
* Estatísticas criadas em índices filtrados.  
* Estatísticas criadas em exibições.  
* Estatísticas criadas em tabelas internas.  
* Estatísticas criadas com índices espaciais ou índices XML.  
  
**Aplica-se a**: [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)] e posterior. 
  
## <a name="when-to-create-statistics"></a><a name="CreateStatistics"></a> Quando criar estatísticas  
 O otimizador de consulta já cria estatísticas das seguintes maneiras:  
  
1.  O otimizador de consulta cria estatísticas para índices em tabelas ou exibições quando o índice é criado. Essas estatísticas são criadas nas colunas de chaves do índice. Se o índice for um índice filtrado, o otimizador de consulta criará estatísticas filtradas no mesmo subconjunto de linhas especificado para o índice filtrado. Para obter mais informações sobre índices filtrados, veja [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md) e [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md).  

    > [!NOTE]
    > Começando com o [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)], as estatísticas não são criadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o otimizador de consulta usa o algoritmo de amostragem padrão para gerar estatísticas. Depois de atualizar um banco de dados com índices particionados, você pode notar uma diferença nos dados de histograma destes índices. Esta alteração no comportamento pode não afetar o desempenho de consulta. Para obter as estatísticas dos índices particionados ao examinar todas as linhas da tabela, use `CREATE STATISTICS` ou `UPDATE STATISTICS` com a cláusula `FULLSCAN`. 
  
2.  O otimizador de consulta cria estatísticas para colunas únicas em predicados de consulta quando [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) estiver ativada.  

Para a maioria das consultas, esses dois métodos para criar estatísticas asseguram um plano de consulta de alta qualidade; em alguns casos, você pode aprimorar os planos de consulta criando estatísticas adicionais com a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) . Essas estatísticas adicionais podem capturar correlações estatísticas que o otimizador de consulta não considera ao criar estatísticas para índices ou colunas únicas. Seu aplicativo pode ter correlações estatísticas adicionais nos dados de tabela que, se calculadas em um objeto de estatísticas, pode permitir que o otimizador de consulta aprimore os planos de consulta. Por exemplo, estatísticas filtradas em um subconjunto de linhas de dados ou estatísticas multicolunas em colunas de predicado de consulta podem aprimorar o plano de consulta.  
  
Ao criar estatísticas com a instrução CREATE STATISTICS, recomendamos manter a opção AUTO_CREATE_STATISTICS ativada de forma que o otimizador de consulta continue criando estatísticas da coluna única rotineiramente para colunas de predicado de consulta. Para obter mais informações sobre predicados de consulta, veja [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
Considere a criação de estatísticas com a instrução CREATE STATISTICS quando alguma das seguintes opções se aplicar:  

* O Orientador de Otimização do [!INCLUDE[ssDE](../../includes/ssde-md.md)] sugere a criação de estatísticas. 
* O predicado de consulta contém várias colunas correlacionadas que ainda não estão no mesmo índice.  
* A consulta faz a seleção em um subconjunto de dados.  
* Há estatísticas ausentes na consulta.  
  
### <a name="query-predicate-contains-multiple-correlated-columns"></a>O predicado de consulta contém várias colunas correlacionadas  
Quando um predicado de consulta contém várias colunas que têm relações e dependências entre colunas, as estatísticas nas várias colunas podem aprimorar o plano de consulta. As estatísticas em várias colunas contêm estatísticas de correlação entre colunas, chamadas *densidades*, que não estão disponíveis em estatísticas de coluna única. As densidades podem aprimorar as estimativas de cardinalidade quando os resultados de consulta dependem de relações de dados entre várias colunas.  
  
Se as colunas já estiverem no mesmo índice, o objeto de estatísticas multicolunas já existirá e não será necessário criá-lo manualmente. Se as colunas ainda não estiverem no mesmo índice, você poderá criar estatísticas multicolunas criando um índice nas colunas ou usando a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md). A manutenção de um índice exige mais recursos do sistema do que a de um objeto de estatísticas. Se o aplicativo não exigir o índice multicolunas, você poderá economizar recursos do sistema criando o objeto de estatísticas sem criar o índice.  
  
Ao criar estatísticas multicolunas, a ordem das colunas na definição do objeto de estatísticas afeta a efetividade de densidades para calcular estimativas de cardinalidade. O objeto de estatísticas armazena densidades para cada prefixo de colunas de chave na definição do objeto. Para obter mais informações sobre densidades, consulte a seção [Densidade](#density) nesta página.  
  
Para criar densidades úteis para estimativas de cardinalidade, as colunas no predicado de consulta devem corresponder a um dos prefixos de colunas na definição do objeto de estatísticas. O exemplo a seguir cria um objeto de estatísticas multicolunas nas colunas `LastName`, `MiddleName`e `FirstName`.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF EXISTS (SELECT name FROM sys.stats  
    WHERE name = 'LastFirst'  
    AND object_ID = OBJECT_ID ('Person.Person'))  
DROP STATISTICS Person.Person.LastFirst;  
GO  
CREATE STATISTICS LastFirst ON Person.Person (LastName, MiddleName, FirstName);  
GO  
```  
  
Neste exemplo, o objeto de estatísticas `LastFirst` apresenta densidades para os seguintes prefixos de coluna: `(LastName)`, `(LastName, MiddleName)` e `(LastName, MiddleName, FirstName)`. A densidade não está disponível para `(LastName, FirstName)`. Se a consulta usar `LastName` e `FirstName` sem usar `MiddleName`, a densidade não estará disponível para estimativas de cardinalidade.  
  
### <a name="query-selects-from-a-subset-of-data"></a>A consulta faz seleções em um subconjunto de dados  
Quando o otimizador de consulta cria estatísticas para colunas únicas e índices, as estatísticas são criadas para os valores em todas as linhas. Quando as consultas fazem seleções em um subconjunto de linhas e esse subconjunto tem uma distribuição de dados exclusiva, as estatísticas filtradas podem aprimorar os planos de consulta. É possível criar estatísticas filtradas usando a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md) com a cláusula [WHERE](../../t-sql/queries/where-transact-sql.md) para definir a expressão de predicado de filtro.  
  
Por exemplo, usando [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)], cada produto na tabela `Production.Product` pertence a uma das quatro categorias na tabela `Production.ProductCategory`: Bicicletas, Componentes, Roupas e Acessórios. Cada categoria possui uma distribuição de dados diferente para peso: as bicicletas pesam de 13,77 a 30, os componentes pesam de 2,12 a 1050,00 com alguns valores NULL, o peso de todas as roupas é NULL e o peso dos acessórios também é NULL.  
  
Usando Bicicletas como um exemplo, as estatísticas filtradas em todos os pesos de bicicleta fornecerão estatísticas mais precisas ao otimizador de consulta e podem melhorar a qualidade do plano de consulta comparadas com as estatísticas de tabela completa ou estatísticas inexistentes na coluna Peso. A coluna de peso das bicicletas é uma boa candidata para estatísticas filtradas, mas não necessariamente para um índice filtrado se o número de pesquisas de peso for relativamente pequeno. O ganho de desempenho que um índice filtrado oferece às pesquisas pode não compensar os custos adicionais com a manutenção e o custo de armazenamento exigidos para adicionar um índice filtrado ao banco de dados.  
  
A instrução a seguir cria as estatísticas filtradas de `BikeWeights` em todas as subcategorias de Bicicletas. A expressão de predicado filtrada define bicicletas enumerando todas as suas subcategorias com a comparação `Production.ProductSubcategoryID IN (1,2,3)`. O predicado não pode usar o nome de categoria Bicicletas porque ele está armazenado na tabela Production.ProductCategory e todas as colunas na expressão de filtro devem estar na mesma tabela.  
  
[!code-sql[StatisticsDDL#FilteredStats2](../../relational-databases/statistics/codesnippet/tsql/statistics_1.sql)]  
  
O otimizador de consulta pode usar as estatísticas filtradas de `BikeWeights` para aprimorar o plano da consulta a seguir, que seleciona todas as bicicletas que pesam mais de `25`.  
  
```sql  
SELECT P.Weight AS Weight, S.Name AS BikeName  
FROM Production.Product AS P  
    JOIN Production.ProductSubcategory AS S   
    ON P.ProductSubcategoryID = S.ProductSubcategoryID  
WHERE P.ProductSubcategoryID IN (1,2,3) AND P.Weight > 25  
ORDER BY P.Weight;  
GO  
```  
  
### <a name="query-identifies-missing-statistics"></a>A consulta identifica estatísticas ausentes  
Se um erro ou outro evento impedir que o otimizador de consulta crie estatísticas, o otimizador criará o plano de consulta sem usar estatísticas. O otimizador de consulta marca as estatísticas como ausentes e tenta gerar as estatísticas novamente na próxima execução da consulta.  
  
As estatísticas ausentes são indicadas como avisos (nome de tabela em texto vermelho) quando o plano de execução de uma consulta é exibido graficamente usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Além disso, o monitoramento da classe de evento **Missing Column Statistics** usando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] indica quando há estatísticas ausentes. Para obter mais informações, veja [Categoria de evento de erros e de avisos &#40;Mecanismo de Banco de Dados&#41;](../../relational-databases/event-classes/errors-and-warnings-event-category-database-engine.md).  
  
 Se houver estatísticas ausentes, execute as seguintes etapas:  
  
* Verifique se [AUTO_CREATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_create_statistics) e [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) estão ativadas.  
* Verifique se o banco de dados não é somente leitura. Se o banco de dados for somente leitura, não será possível salvar um novo objeto de estatística.  
* Crie as estatísticas ausentes usando a instrução [CREATE STATISTICS](../../t-sql/statements/create-statistics-transact-sql.md).  
  
Quando as estatísticas em um banco de dados somente leitura ou um instantâneo somente leitura estão ausentes ou obsoletas, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria e mantém estatísticas temporárias no **tempdb**. Quando o [!INCLUDE[ssDE](../../includes/ssde-md.md)] cria estatísticas temporárias, o nome das estatísticas é anexado com o sufixo *_readonly_database_statistic* para diferenciar as estatísticas temporárias de estatísticas permanentes. O sufixo *_readonly_database_statistic* fica reservado para estatísticas geradas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. É possível criar e reproduzir scripts para as estatísticas temporárias em um banco de dados de leitura-gravação. Quando em script, o [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] altera o sufixo do nome das estatísticas de *_readonly_database_statistic* para *_readonly_database_statistic_scripted*.  
  
Somente o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode criar e atualizar estatísticas temporárias. No entanto, você pode excluir estatísticas temporárias e monitorar as propriedades de estatísticas que usam as mesmas ferramentas que você utiliza para estatísticas permanentes:  
  
* Exclua estatísticas temporárias usando a instrução [DROP STATISTICS](../../t-sql/statements/drop-statistics-transact-sql.md).  
* Para monitorar as estatísticas, use as exibições de catálogo **[sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)** e **[sys.stats_columns](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)** . **sys_stats** inclui a coluna, **is_temporary** para indicar quais estatísticas são permanentes e quais são temporárias.  
  
 Como as estatísticas temporárias são armazenadas em **tempdb**, uma reinicialização do serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] faz com que todas as estatísticas temporárias desapareçam.  
    
## <a name="when-to-update-statistics"></a><a name="UpdateStatistics"></a> Quando atualizar estatísticas  
 O otimizador de consulta determina quando as estatísticas podem estar desatualizadas e as atualiza quando forem necessárias para um plano de consulta. Em alguns casos, você pode aprimorar o plano de consulta e, portanto, o desempenho da consulta por meio da atualização mais frequente das estatísticas do que quando [AUTO_UPDATE_STATISTICS](../../t-sql/statements/alter-database-transact-sql-set-options.md#auto_update_statistics) está ativada. Você pode atualizar estatísticas com a instrução UPDATE STATISTICS ou o procedimento armazenado sp_updatestats.  
  
 A atualização de estatísticas assegura que as consultas sejam compiladas com estatísticas atualizadas. Porém, a atualização de estatísticas faz com que as consultas sejam recompiladas. É recomendável não atualizar estatísticas com muita frequência porque existe uma compensação de desempenho entre o aprimoramento dos planos de consulta e o tempo necessário para recompilar consultas. As compensações específicas dependem do seu aplicativo.  
  
 Quando atualizar estatísticas com UPDATE STATISTICS ou sp_updatestats, recomendamos manter a opção AUTO_UPDATE_STATISTICS ativada de modo que o otimizador de consulta continue a atualizar estatísticas periodicamente. Para obter mais informações sobre como atualizar estatísticas em uma coluna, um índice, uma tabela ou uma exibição indexada, veja [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md). Para obter informações sobre como atualizar estatísticas de todas as tabelas definidas pelo usuário e internas no banco de dados, veja o procedimento armazenado [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md).  
  
 Para determinar quando as estatísticas foram atualizadas pela última vez, use as funções [sys.dm_db_stats_properties](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md) ou [STATS_DATE](../../t-sql/functions/stats-date-transact-sql.md).  
  
 Considere a atualização de estatísticas nas seguintes condições:  
  
* Os tempos de execução de consulta estão lentos.  
* As operações de inserção ocorrem em colunas de chaves crescentes ou decrescentes.  
* Após operações de manutenção.  

### <a name="query-execution-times-are-slow"></a>Os tempos de execução de consulta estão lentos  
 Se os tempos de resposta de consultas estiverem lentos ou imprevisíveis, verifique se as consultas têm estatísticas atualizadas antes de executar as etapas adicionais de solução de problemas.  
  
### <a name="insert-operations-occur-on-ascending-or-descending-key-columns"></a>As operações de inserção ocorrem em Colunas de Chaves crescentes ou decrescentes  
 As estatísticas em Colunas de Chaves crescentes ou decrescentes, como colunas IDENTITY ou colunas de carimbo de data/hora em tempo real, podem exigir atualizações de estatísticas mais frequentes do que as executadas pelo otimizador de consulta. As operações de inserção acrescentam novos valores às colunas crescentes ou decrescentes. O número de linhas adicionadas pode ser muito pequeno para disparar uma atualização de estatísticas. Se as estatísticas não estiverem atualizadas e as consultas fizerem seleções nas linhas adicionadas mais recentemente, as estatísticas atuais não terão estimativas de cardinalidade para obter esses novos valores. Isso pode resultar em estimativas de cardinalidade imprecisas e lentidão no desempenho de consulta.  
  
 Por exemplo, uma consulta que faz seleções em ordens de venda com as datas mais recentes terá estimativas de cardinalidade imprecisas, se as estatísticas não forem atualizadas para incluir estimativas de cardinalidade dessas ordens de venda.  
  
### <a name="after-maintenance-operations"></a>Após operações de manutenção  
 Considere a atualização de estatísticas depois de executar procedimentos de manutenção que alteram a distribuição de dados, como truncar uma tabela ou executar uma inserção em massa de uma porcentagem grande das linhas. Isso pode evitar futuros atrasos no processamento de consultas enquanto elas aguardam atualizações de estatísticas automáticas.  
  
 Operações como reconstrução, desfragmentação ou reorganização de um índice não alteram a distribuição de dados. Portanto, não é necessário atualizar estatísticas depois de executar as operações [ALTER INDEX REBUILD](../../t-sql/statements/alter-index-transact-sql.md#rebuilding-indexes), [DBCC DBREINDEX](../../t-sql/database-console-commands/dbcc-dbreindex-transact-sql.md), [DBCC INDEXDEFRAG](../../t-sql/database-console-commands/dbcc-indexdefrag-transact-sql.md) ou [ALTER INDEX REORGANIZE](../../t-sql/statements/alter-index-transact-sql.md#reorganizing-indexes). O otimizador de consulta atualiza estatísticas quando você reconstrói um índice em uma tabela ou exibição com ALTER INDEX REBUILD ou DBCC DBREINDEX; no entanto, essa atualização de estatísticas é um subproduto da recriação do índice. O otimizador de consulta não atualiza estatísticas depois de operações DBCC INDEXDEFRAG ou ALTER INDEX REORGANIZE. 
 
> [!TIP]
> Começando com o [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] SP1 CU4, use a opção PERSIST_SAMPLE_PERCENT de [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md) ou [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md) a fim de definir e reter uma porcentagem de amostragem específica para atualizações estatísticas subsequentes que não especificam explicitamente uma porcentagem de amostragem.

### <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas

Aproveite soluções como a [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.
  
##  <a name="queries-that-use-statistics-effectively"></a><a name="DesignStatistics"></a> Consultas que usam estatísticas de modo eficiente  
 Algumas implementações de consulta, como variáveis locais e expressões complexas no predicado de consulta, podem gerar planos de consulta de qualidade inferior. O cumprimento das diretrizes de design de consulta para o uso eficiente de estatísticas pode ajudar a evitar esse problema. Para obter mais informações sobre predicados de consulta, veja [Critério de pesquisa &#40;Transact-SQL&#41;](../../t-sql/queries/search-condition-transact-sql.md).  
  
 Você pode melhorar planos de consulta aplicando diretrizes de design de consulta que usam estatísticas de modo eficiente para aprimorar *estimativas de cardinalidade* para expressões, variáveis e funções usadas em predicados de consulta. Quando o otimizador de consulta não souber o valor de uma expressão, variável ou função, ele não saberá qual valor deve ser pesquisado no histograma e, portanto, não poderá recuperar a estimativa ideal de cardinalidade do histograma. Em vez disso, o otimizador de consulta baseia a estimativa de cardinalidade no número médio de linhas por valor distinto de todas as linhas de amostra no histograma. Isso gera estimativas de cardinalidade de qualidade inferior e pode prejudicar o desempenho de consulta. Para saber mais sobre histogramas, confira a seção [histograma](#histogram) nessa página ou em [sys.dm_db_stats_histogram](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md).
  
 As diretrizes a seguir descrevem como escrever consultas para melhorar planos de consulta por meio do aprimoramento das estimativas de cardinalidade.  
  
### <a name="improving-cardinality-estimates-for-expressions"></a>Aprimorando estimativas de cardinalidade para expressões  
Para aprimorar as estimativas de cardinalidade para expressões, siga estas diretrizes:  
  
* Sempre que possível, simplifique expressões com constantes. O otimizador de consulta não avalia todas as funções e expressões que contêm constantes, antes de determinar as estimativas de cardinalidade. Por exemplo, simplifique a expressão `ABS(-100)` para `100`.  
  
* Se a expressão usar muitas variáveis, considere a criação de uma coluna computada para a expressão e crie estatísticas ou um índice na coluna computada. Por exemplo, o predicado de consulta `WHERE PRICE + Tax > 100` poderá ter uma estimativa de cardinalidade melhor se você criar uma coluna computada para a expressão `Price + Tax`.  
  
### <a name="improving-cardinality-estimates-for-variables-and-functions"></a>Aprimorando estimativas de cardinalidade para variáveis e funções  
Para melhorar as estimativas de cardinalidade para variáveis e funções, siga estas diretrizes:  
  
* Se o predicado de consulta usar uma variável local, considere reescrever a consulta para usar um parâmetro em vez de uma variável local. O valor de uma variável local não é conhecido quando o otimizador de consulta cria o plano de execução de consulta. Quando uma consulta usa um parâmetro, o otimizador de consulta usa a estimativa de cardinalidade para o primeiro valor de parâmetro real transmitido ao procedimento armazenado.  
  
* Considere o uso de uma tabela padrão ou uma tabela temporária para manter os resultados de funções com valor de tabela de várias instruções (mstvf). O otimizador de consulta não cria estatísticas para funções com valor de tabela de várias instruções. Com essa abordagem, o otimizador de consulta pode criar estatísticas nas colunas de tabela e usá-las para criar um plano de consulta melhor.  
  
* Considere o uso de uma tabela padrão ou uma tabela temporária como uma substituição para variáveis de tabela. O otimizador de consulta não cria estatísticas para variáveis de tabela. Com essa abordagem, o otimizador de consulta pode criar estatísticas nas colunas de tabela e usá-las para criar um plano de consulta melhor. Há compensações ao optar pelo uso de uma tabela temporária ou de uma variável de tabela; as variáveis de tabela usadas em procedimentos armazenados causam menos recompilações do procedimento armazenado que as tabelas temporárias. Dependendo do aplicativo, o uso de uma tabela temporária em vez de uma variável de tabela pode não melhorar o desempenho.  
  
* Se um procedimento armazenado contiver uma consulta que usa um parâmetro transmitido, evite alterar o valor de parâmetro no procedimento armazenado antes de usá-lo na consulta. As estimativas de cardinalidade da consulta se baseiam no valor de parâmetro transmitido, não no valor atualizado. Para evitar alterar o valor do parâmetro, você pode reescrever a consulta para usar dois procedimentos armazenados.  
  
     Por exemplo, o procedimento armazenado `Sales.GetRecentSales` a seguir altera o valor do parâmetro `@date` quando `@date` é NULL.  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
    AS BEGIN  
        IF @date IS NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
     Se a primeira chamada do procedimento armazenado `Sales.GetRecentSales` transmitir NULL para o parâmetro `@date`, o otimizador de consulta compilará o procedimento armazenado com a estimativa de cardinalidade para `@date = NULL`, embora o predicado de consulta não seja chamado com `@date = NULL`. Essa estimativa de cardinalidade pode ser significativamente diferente do número de linhas no resultado de consulta real. Como resultado, o otimizador de consulta pode escolher um plano de consulta de qualidade inferior. Para evitar isso, você pode reescrever o procedimento armazenado em dois procedimentos da seguinte maneira:  
  
    ```sql  
    USE AdventureWorks2012;  
    GO  
    IF OBJECT_ID ( 'Sales.GetNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNullRecentSales (@date datetime)  
    AS BEGIN  
        IF @date is NULL  
            SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
        EXEC Sales.GetNonNullRecentSales @date;  
    END  
    GO  
    IF OBJECT_ID ( 'Sales.GetNonNullRecentSales', 'P') IS NOT NULL  
        DROP PROCEDURE Sales.GetNonNullRecentSales;  
    GO  
    CREATE PROCEDURE Sales.GetNonNullRecentSales (@date datetime)  
    AS BEGIN  
        SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
        WHERE h.SalesOrderID = d.SalesOrderID  
        AND h.OrderDate > @date  
    END  
    GO  
    ```  
  
### <a name="improving-cardinality-estimates-with-query-hints"></a>Aprimorando estimativas de cardinalidade com dicas de consulta  
 Para aprimorar estimativas de cardinalidade para variáveis locais, use as dicas de consulta `OPTIMIZE FOR <value>` ou `OPTIMIZE FOR UNKNOWN` com RECOMPILE. Para obter mais informações, veja [Dicas de consulta &#40;Transact-SQL&#41;](../../t-sql/queries/hints-transact-sql-query.md).  
  
 Para alguns aplicativos, a recompilação da consulta toda vez que ela é executada pode levar muito tempo. A dica de consulta `OPTIMIZE FOR` poderá ajudar, mesmo que você não use a opção `RECOMPILE`. Por exemplo, você poderia adicionar uma opção `OPTIMIZE FOR` ao procedimento armazenado Sales.GetRecentSales para especificar uma data. O exemplo a seguir adiciona a opção `OPTIMIZE FOR` ao procedimento Sales.GetRecentSales.  
  
```sql  
USE AdventureWorks2012;  
GO  
IF OBJECT_ID ( 'Sales.GetRecentSales', 'P') IS NOT NULL  
    DROP PROCEDURE Sales.GetRecentSales;  
GO  
CREATE PROCEDURE Sales.GetRecentSales (@date datetime)  
AS BEGIN  
    IF @date is NULL  
        SET @date = DATEADD(MONTH, -3, (SELECT MAX(ORDERDATE) FROM Sales.SalesOrderHeader))  
    SELECT * FROM Sales.SalesOrderHeader h, Sales.SalesOrderDetail d  
    WHERE h.SalesOrderID = d.SalesOrderID  
    AND h.OrderDate > @date  
    OPTION ( OPTIMIZE FOR ( @date = '2004-05-01 00:00:00.000'))  
END;  
GO  
```  
  
### <a name="improving-cardinality-estimates-with-plan-guides"></a>Aprimorando estimativas de cardinalidade com guias de plano  
 Para alguns aplicativos, é possível que as diretrizes de design de consulta não se apliquem porque você não pode alterar a consulta ou porque o uso da dica de consulta RECOMPILE pode causar muitas recompilações. Você pode usar guias de plano para especificar outras dicas, como USE PLAN, a fim de controlar o comportamento da consulta ao investigar alterações do aplicativo com o fornecedor do aplicativo. Para obter mais informações sobre guias de plano, consulte [Plan Guides](../../relational-databases/performance/plan-guides.md).  
  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)   
 [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)   
 [sp_updatestats &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-updatestats-transact-sql.md)   
 [DBCC SHOW_STATISTICS &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-show-statistics-transact-sql.md)   
 [Opções ALTER DATABASE SET &#40;Transact-SQL&#41;](../../t-sql/statements/alter-database-transact-sql-set-options.md)   
 [DROP STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/drop-statistics-transact-sql.md)   
 [CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)   
 [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)   
 [Criar índices filtrados](../../relational-databases/indexes/create-filtered-indexes.md)   
 [Controlando o comportamento das atualizações automáticas de estatísticas (AUTO_UPDATE_STATISTICS) no SQL Server](https://support.microsoft.com/help/2754171)   
 [STATS_DATE &#40;Transact-SQL&#41;](../../t-sql/functions/stats-date-transact-sql.md)   
 [sys.dm_db_stats_properties &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-properties-transact-sql.md)   
 [sys.dm_db_stats_histogram &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-stats-histogram-transact-sql.md)  
 [sys.stats](../../relational-databases/system-catalog-views/sys-stats-transact-sql.md)  
 [sys.stats_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-stats-columns-transact-sql.md)    
 [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)