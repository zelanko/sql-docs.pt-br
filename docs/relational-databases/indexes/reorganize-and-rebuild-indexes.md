---
title: Reorganizar e recompilar índices | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2019
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
f1_keywords:
- sql13.swb.index.rebuild.f1
- sql13.swb.indexproperties.fragmentation.f1
- sql13.swb.index.reorg.f1
helpviewer_keywords:
- large object defragmenting
- indexes [SQL Server], reorganizing
- index reorganization [SQL Server]
- reorganizing indexes
- defragmenting large object data types
- index fragmentation [SQL Server]
- index rebuilding [SQL Server]
- rebuilding indexes
- indexes [SQL Server], rebuilding
- defragmenting indexes
- nonclustered indexes [SQL Server], defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
- LOB data [SQL Server], defragmenting
- clustered indexes, defragmenting
ms.assetid: a28c684a-c4e9-4b24-a7ae-e248808b31e9
author: pmasl
ms.author: mikeray
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: cd844947b93e17684643fe95b5c51335af81b473
ms.sourcegitcommit: c98c6e33d04d4a1888db7dbe89cb0b1bb3a66418
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2019
ms.locfileid: "74249749"
---
# <a name="reorganize-and-rebuild-indexes"></a>Reorganizar e recompilar índices

[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Este artigo descreve como reorganizar ou recompilar o índice fragmentado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] ou o [!INCLUDE[tsql](../../includes/tsql-md.md)]. O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] modifica os índices automaticamente sempre que são realizadas operações de entrada, atualização ou exclusão nos dados subjacentes. No decorrer do tempo, essas modificações podem fazer com que as informações do índice sejam dispersadas pelo banco de dados (fragmentadas). A fragmentação ocorre quando os índices têm páginas nas quais a ordem lógica, com base no valor de chave, não corresponde à ordem física do arquivo de dados. Os índices com fragmentação pesada podem degradar o desempenho da consulta e causar lentidão de resposta do aplicativo, especialmente nas operações de exame.

Você pode solucionar a fragmentação de índice reorganizando ou recriando um índice. Para índices particionados criados em um esquema de partição, é possível usar qualquer um desses métodos em um índice completo ou em uma única partição de índice:

- **Reorganizar um índice** usa recursos mínimos do sistema e é uma operação online. Isso significa que os bloqueios de tabela de longo prazo não são mantidos e que as consultas ou atualizações da tabela subjacente podem continuar durante a transação `ALTER INDEX REORGANIZE`.
  - Para índices **rowstore**, ela desfragmenta o nível folha de índices clusterizados e não clusterizados em tabelas e exibições, reordenando fisicamente as páginas de nível folha para que correspondam à ordem lógica, da esquerda para a direita, dos nós folha. A reorganização também compacta as páginas de índice. A compactação baseia-se no valor do fator de preenchimento existente. Para exibir a configuração do fator de preenchimento, use [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).
  - Ao usar índices **columnstore**, é possível que, depois de carregar os dados, o armazenamento Delta tenha vários rowgroups pequenos. A reorganização do índice columnstore força todos os rowgroups no columnstore e, em seguida, combina os rowgroups em menos RowGroups com mais filas. A operação de reorganização removerá também as linhas que foram excluídas do columnstore. Inicialmente, a reorganização exigirá recursos de CPU adicionais para compactar os dados, o que pode reduzir o desempenho geral do sistema. No entanto, assim que os dados forem compactados, o desempenho de consulta poderá aumentar.

- **A recriação de um índice** descarta e recria o índice. Dependendo do tipo de índice e a versão [!INCLUDE[ssDE](../../includes/ssde-md.md)], isso pode ser feito online ou offline.
  - Para índices **rowstore**, isso remove a fragmentação, recupera espaço em disco ao compactar as páginas com base na configuração do fator de preenchimento especificada ou existente, e reclassifica as linhas do índice em páginas contíguas. Quando `ALL` é especificado, todos os índices da tabela são descartados e recriados em uma única transação. As restrições de chave estrangeira não precisam ser descartadas com antecedência. Quando índices com 128 extensões ou mais são recriados, o [!INCLUDE[ssDE](../../includes/ssde-md.md)] adia as desalocações de página atuais e seus bloqueios associados até depois da confirmação da transação.
  - Para **índices** columnstore, a recompilação remove a fragmentação, move todas as linhas para o columnstore e recupera o espaço em disco ao excluir fisicamente as linhas que foram excluídas logicamente da tabela. Iniciando com [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)], normalmente, não é necessário recompilar o índice columnstore porque `REORGANIZE` executa as etapas básicas de uma recompilação em segundo plano como uma operação online.

Nas versões anteriores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], às vezes, era possível recriar um índice não clusterizado do rowstore para corrigir as inconsistências causadas por falhas de hardware.
Iniciando com o [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], ainda é possível reparar essas inconsistências entre o índice e o índice clusterizado recriando um índice não clusterizado offline. Entretanto, não é possível reparar inconsistências de índice não clusterizado recriando o índice online, porque o mecanismo de recriação online usará o índice não clusterizado existente como base para a recriação e, portanto, a inconsistência persistirá. A recriação do índice offline poderá forçar, algumas vezes, um exame do índice clusterizado (ou heap) e, consequentemente, remover a inconsistência. Para garantir uma recompilação do índice clusterizado, remova e recrie o índice não clusterizado. Como nas versões anteriores, é recomendável que a recuperação de inconsistências seja feita com a restauração dos dados afetados de um backup; porém, talvez seja possível reparar as inconsistências do índice recriando o índice não clusterizado offline. Para obter mais informações, veja [DBCC CHECKDB &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-checkdb-transact-sql.md).

## <a name="Fragmentation"></a> Detectando a fragmentação

A primeira etapa para optar pelo método de fragmentação a ser usado é analisar o índice para determinar o grau de fragmentação.

### <a name="detecting-fragmentation-on-rowstore-indexes"></a>Detectando a fragmentação em índices de rowstore

Usando a função de sistema [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md), você pode detectar a fragmentação em um índice específico, em todos os índices de uma tabela ou exibição indexada, em todos os índices de um banco de dados ou em todos os índices de todos os bancos de dados. Para índices particionados, **sys.dm_db_index_physical_stats** também fornece informações de fragmentação por partição.

O conjunto de resultados retornado pela função **sys.dm_db_index_physical_stats** inclui as colunas a seguir:

|Coluna|DESCRIÇÃO|
|------------|-----------------|
|**avg_fragmentation_in_percent**|Porcentagem de fragmentação lógica (páginas fora de ordem no índice).|
|**fragment_count**|Número de fragmentos (páginas folha fisicamente consecutivas) do índice.|
|**avg_fragment_size_in_pages**|Número médio de páginas em um fragmento de índice.|

Depois que o grau de fragmentação for conhecido, use a tabela a seguir para determinar o melhor método para corrigir a fragmentação.

|Valor**avg_fragmentation_in_percent**|Instrução corretiva|
|-----------------------------------------------|--------------------------|
|> 5% e < = 30%|ALTER INDEX REORGANIZE|
|> 30%|ALTER INDEX REBUILD WITH (ONLINE = ON) <sup>1</sup>|

<sup>1</sup> A recompilação de um índice pode ser executada online ou offline. A reorganização de um índice sempre é executada online. Para atingir disponibilidade semelhante à opção de reorganização, recrie índices online. Para obter mais informações, consulte [Perform Index Operations Online](../../relational-databases/indexes/perform-index-operations-online.md).

> [!TIP]
> Esses valores fornecem uma orientação aproximada para determinar o ponto em que você deve mudar entre `ALTER INDEX REORGANIZE` e `ALTER INDEX REBUILD`. Contudo, os valores reais podem variar de acordo com o caso. É importante que você experimente para poder determinar o melhor limite para um ambiente. Por exemplo, se um determinado índice for usado principalmente para operações de verificação, o desempenho delas poderá ser aprimorado pela remoção da fragmentação. O benefício de desempenho é menos perceptível para índices que são usados principalmente para operações de busca. Da mesma forma, remover a fragmentação em um heap (uma tabela sem índice clusterizado) é especialmente útil para operações de verificação de índice não clusterizado, mas tem pouco efeito em operações de pesquisa.

Em geral, níveis muito baixos de fragmentação (menos de 5 por cento) não devem ser resolvidos por nenhum desses comandos, pois o benefício da remoção de uma pequena quantidade de fragmentação é quase sempre amplamente excedido pelo custo da reorganização ou da recriação do índice. Para obter mais informações sobre `ALTER INDEX REORGANIZE` e `ALTER INDEX REBUILD`, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).

> [!NOTE]
> A recriação ou reorganização de índices rowstore pequenos geralmente não reduz a fragmentação. As páginas de índices pequenos às vezes são armazenadas em extensões mistas. Extensões mistas são compartilhadas por até oito objetos, portanto, a fragmentação em um índice pequeno pode não ser reduzida após a reorganização ou recriação.

### <a name="detecting-fragmentation-on-columnstore-indexes"></a>Detectando a fragmentação em índices de columnstore

Usando o DMV [sys.dm_db_column_store_row_group_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-column-store-row-group-physical-stats-transact-sql.md), você pode determinar a porcentagem de linhas excluídas, que é uma boa medida para a fragmentação em um rowgroup. Use essas informações para computar a fragmentação em um índice específico, todos os índices em uma tabela, todos os índices em um banco de dados ou todos os índices em todos os bancos de dados.

O conjunto de resultados retornado pelo DMV **sys.dm_db_column_store_row_group_physical_stats** inclui as seguintes colunas:

|Coluna|DESCRIÇÃO|
|------------|-----------------|
|**total_rows**|Número de linhas armazenadas fisicamente no grupo de linhas. Para grupos de linhas compactados, isso inclui as linhas marcadas como excluídas.|
|**deleted_rows**|Número de linhas fisicamente armazenadas em um grupo de linhas compactado que são marcadas para exclusão. 0 para grupos de linhas que estão no repositório Delta.|

Isso pode ser usado para calcular a fragmentação usando a fórmula `100*(ISNULL(deleted_rows,0))/NULLIF(total_rows,0)`. Depois que o grau de fragmentação for conhecido, use a tabela a seguir para determinar o melhor método para corrigir a fragmentação.

|**fragmentação calculada em valor** percentual|Aplica-se à versão|Instrução corretiva|
|-----------------------------------------------|--------------------------|--------------------------|
|> = 20%|[!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e [!INCLUDE[ssSQL14](../../includes/sssql14-md.md)]|ALTER INDEX REBUILD|
|> = 20%|A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)]|ALTER INDEX REORGANIZE|

## <a name="index-defragmentation-considerations"></a>Considerações sobre fragmentação de índice

Em determinadas condições, recompilar um índice clusterizado recompilará automaticamente todo índice não clusterizado que faça referência à chave de clustering, se os identificadores físicos ou lógicos contidos nos registros de índice não clusterizados precisam ser alterados.

Cenários que requerem que todos os índices rowstore não clusterizados sejam automaticamente recompilados em uma tabela:

- Criar um índice clusterizado em uma tabela
- Remover um índice clusterizado, fazendo com que a tabela seja armazenada como um heap
- Alterar a chave de clustering para incluir ou excluir colunas

Cenários que não requerem que todos os índices rowstore não clusterizados sejam automaticamente recompilados em uma tabela:

- Recompilar um índice clusterizado exclusivo
- Recompilar um índice clusterizado não exclusivo
- Alterar o esquema de índice (assim como ao aplicar um esquema de particionamento a um índice clusterizado) ou mover o índice clusterizado para um grupo de arquivos diferente

> [!IMPORTANT]
> Um índice não poderá ser reorganizado ou recriado se o grupo de arquivos no qual ele está localizado estiver offline ou definido como somente leitura. Quando a palavra-chave ALL for especificada e um ou mais índices estiver em um grupo de arquivos offline ou somente leitura, a instrução falhará.
>
> Enquanto ocorre uma reconstrução de índice, a mídia física deve ter espaço suficiente para armazenar duas cópias do índice. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exclui o índice original.

Quando `ALL` for especificado com a instrução `ALTER INDEX`, os índices relacionais, clusterizados e não clusterizados e os índices XML da tabela serão reorganizados.

### <a name="considerations-specific-to-rebuilding-a-columnstore-index"></a>Considerações específicas para recompilar um índice columnstore

Ao recriar um índice columnstore, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] lê todos os dados do índice columnstore original, incluindo o armazenamento Delta. Combina os dados em novos rowgroups e compacta os rowgroups em columnstore. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] desfragmenta o columnstore excluindo fisicamente as linhas que foram excluídas logicamente da tabela; os bytes excluídos são recuperados no disco.

Recriar uma partição em vez de toda a tabela:

- Recriar a tabela inteira é uma tarefa demorada se o índice é grande, e isso exige espaço em disco suficiente para armazenar uma cópia adicional do índice durante a recriação. Geralmente, é necessário recriar apenas a partição mais recentemente usada.
- Em tabelas particionadas, não é necessário recriar todo o índice columnstore, pois é provável que a fragmentação ocorra apenas nas partições que foram modificadas recentemente. As tabelas de fatos e de dimensões grandes geralmente são particionadas para executar operações de backup e gerenciamento em partes da tabela.

Recriar uma partição após operações DML pesadas:

- Recriar uma partição desfragmentará a partição e reduzirá o armazenamento em disco. Essa recriação excluirá todas as linhas do columnstore marcadas para exclusão e moverá todos os rowgroups do armazenamento Delta para o columnstore. Observe que pode haver várias rowgroups no armazenamento Delta, que possuem menos de um milhão de linhas.

Recriar uma partição após carregar dados:

- Isso garante que todos dados sejam armazenados no columnstore. Quando os processos atuais carregam menos de 100 mil linhas cada um na mesma partição em simultâneo, a partição pode acabar com vários armazenamento Delta. A recriação moverá todas as linhas do armazenamento Delta para o columnstore.

### <a name="considerations-specific-to-reorganizing-a-columnstore-index"></a>Considerações específicas para reorganizar um índice columnstore

Ao reorganizar um índice columnstore, [!INCLUDE[ssde_md](../../includes/ssde_md.md)] compacta cada rowgroup delta FECHADO no columnstore como um rowgroup compactado. A partir do [!INCLUDE[ssSQL15](../../includes/sssql15-md.md)] e no [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)], o comando `REORGANIZE` executa as seguintes otimizações adicionais de desfragmentação online:

- Remove fisicamente linhas de um grupo de linhas quando 10% ou mais linhas foram excluídas logicamente. Os bytes excluídos são recuperados na mídia física. Por exemplo, se um grupo de linhas compactado de 1 milhão de linhas tiver 100 mil linhas excluídas, o SQL Server removerá as linhas excluídas e recompactará o rowgroup com 900 mil linhas. Ele salva no armazenamento removendo as linhas excluídas.

- Combina um ou mais rowgroups compactados para aumentar linhas por rowgroup até o máximo de 1.024.576 linhas. Por exemplo, se você importar em massa cinco lotes de 102.400 linhas, obterá cinco rowgroups compactados. Se você executar REORGANIZE, esses rowgroups serão mesclados em um grupo de linhas compactado de 512 mil linhas de tamanho. Isso pressupõe que não havia nenhuma limitação de tamanho ou memória de dicionário.
- Para rowgroups em que 10% ou mais linhas foram excluídas logicamente, o [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tenta combinar esse grupo de linhas com um ou mais rowgroups. Por exemplo, o rowgroup 1 é compactado com 500 mil linhas e o rowgroup 21 é compactado com o máximo de 1.048.576 linhas. O rowgroup 21 tem 60% das linhas excluídas, o que deixa 409.830 linhas. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] favorece combinar esses dois rowgroups para compactar um novo rowgroup com 909.830 linhas.

Depois de executar os carregamentos de dados, você poderá ter vários rowgroups pequenos no armazenamento Delta. Use `ALTER INDEX REORGANIZE` para forçar todos os rowgroups no índice columnstore e, em seguida, combinar os rowgroups em rowgroups menores com mais linhas. A operação de reorganização removerá também as linhas que foram excluídas do columnstore.

## <a name="Restrictions"></a> Limitações e restrições

Índices rowstore com mais de 128 extensões são recriados em duas fases separadas: lógica e física. Na fase lógica, as unidades de alocação existentes usadas pelo índice são marcadas para desalocação, as linhas de dados são copiadas, ordenadas e, depois, movidas para novas unidades de alocação criadas para armazenar o índice recriado. Na fase física, as unidades de alocação previamente marcadas para desalocação são fisicamente canceladas em transações curtas que ocorrem em segundo plano e que não exigem muitos bloqueios. Para obter mais informações sobre as extensões, consulte o [Guia de arquitetura de páginas e extensões](../../relational-databases/pages-and-extents-architecture-guide.md).

A instrução `ALTER INDEX REORGANIZE` exige que o arquivo de dados que contém o índice tenha espaço disponível, pois a operação só pode alocar páginas de trabalho temporárias no mesmo arquivo, não em outro arquivo no grupo de arquivos. Portanto, embora o grupo de arquivos possa ter páginas livres disponíveis, o usuário ainda poderá se deparar com o erro 1105:`Could not allocate space for object '###' in database '###' because the '###' filegroup is full. Create disk space by deleting unneeded files, dropping objects in the filegroup, adding additional files to the filegroup, or setting autogrowth on for existing files in the filegroup.`

> [!WARNING]
> É possível criar e reconstruir índices não alinhados em uma tabela com mais de 1.000 partições, mas não há suporte para isso. Fazer isso pode provocar degradação do desempenho ou consumo excessivo de memória durante essas operações. A Microsoft recomenda usar índices alinhados apenas quando o número de partições for maior que 1.000.

Um índice não poderá ser reorganizado ou recriado se o grupo de arquivos no qual ele está localizado estiver **offline** ou definido como **somente leitura**. Quando a palavra-chave `ALL` for especificada e um ou mais índices estiver em um grupo de arquivos offline ou somente leitura, a instrução falhará.

Quando um índice for **criado** ou **reconstruído** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as estatísticas serão criadas ou atualizadas por meio do exame de todas as linhas da tabela. No entanto, começando com o [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)], as estatísticas não são criadas nem atualizadas por meio do exame de todas as linhas da tabela quando um índice particionado é criado ou reconstruído. Em vez disso, o Otimizador de consultas usa o algoritmo de amostragem padrão para gerar essas estatísticas. Para obter as estatísticas dos índices particionados ao examinar todas as linhas da tabela, use `CREATE STATISTICS` ou `UPDATE STATISTICS` com a cláusula `FULLSCAN`.

Quando um índice é **reorganizado** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], as estatísticas não são atualizadas.

Um índice não pode ser reorganizado quando `ALLOW_PAGE_LOCKS` está definido como OFF.

Até [!INCLUDE[ssSQL17](../../includes/sssql17-md.md)], a recriação de um índice columnstore clusterizado é uma operação offline. O [!INCLUDE[ssde_md](../../includes/ssde_md.md)] tem que adquirir um bloqueio exclusivo na tabela ou na partição durante a recompilação. Os dados estão offline e não estão disponíveis durante a recompilação mesmo ao usar `NOLOCK`, RCSI (isolamento de instantâneo com leitura confirmada) ou isolamento de instantâneo.
A partir do [!INCLUDE[sql-server-2019](../../includes/sssqlv15-md.md)],um índice columnstore clusterizado pode ser recompilado usando a opção `ONLINE=ON`.

Para uma tabela do SQL Data Warehouse do Azure com um índice columnstore clusterizado ordenado, `ALTER INDEX REBUILD` reclassificará os dados usando TempDB. Monitore o TempDB durante operações de recompilação. Se você precisar de mais espaço de TempDB, aumente o data warehouse. Diminua quando a recompilação do índice for concluída.

Para uma tabela do SQL Data Warehouse do Azure com um índice columnstore clusterizado ordenado, o `ALTER INDEX REORGANIZE` não reclassificará os dados. Para reclassificar os dados, use `ALTER INDEX REBUILD`.

## <a name="Security"></a> Segurança

### <a name="Permissions"></a> Permissões

Requer a permissão `ALTER` na tabela ou exibição. O usuário deve ser um membro de pelo menos uma das seguintes funções:

- Função de banco de dados **db_ddladmin**<sup>1</sup>
- Função de banco de dados **db_owner**
- função de servidor **sysadmin**

<sup>1</sup>A função de banco de dados **db_ddladmin** é a [menos privilegiada](/windows-server/identity/ad-ds/plan/security-best-practices/implementing-least-privilege-administrative-models).

## <a name="SSMSProcedureFrag"></a> Verificar a fragmentação de índice usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

> [!NOTE]
> [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] não pode ser usado para computar a fragmentação de índices columnstore no SQL Server e não pode ser usado para computar a fragmentação de nenhum índice no Banco de Dados SQL do Azure. Use o exemplo [!INCLUDE[tsql](../../includes/tsql-md.md)][a seguir](#TsqlProcedureFrag).

1. No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja verificar a fragmentação de um índice.
2. Expanda a pasta **Tabelas** .
3. Expanda a tabela na qual você deseja verificar a fragmentação de um índice.
4. Expanda a pasta **Índices** .
5. Clique com o botão direito do mouse no índice cuja fragmentação você deseja verificar e selecione **Propriedades**.
6. Em **Selecione uma página**, selecione **Fragmentação**.

As informações a seguir estão disponíveis na página **Fragmentação** :

|Valor|DESCRIÇÃO|
|---|---|
|**Preenchimento da página**|Indica o preenchimento médio das páginas do índice, como uma porcentagem. 100% significa que as páginas de índice estão completamente preenchidas. 50% significa que, em média, cada página do índice está preenchida pela metade.|
|**Fragmentação total**|A porcentagem de fragmentação lógica. Isso indica o número de páginas em um índice que não estão armazenadas em ordem.|
|**Tamanho médio da linha**|O tamanho médio de uma linha de nível folha.|
|**Profundidade**|O número de níveis no índice, inclusive o nível folha.|
|**Registros encaminhados**|O número de registros em um heap com ponteiros encaminhados a outro local de dados (Esse estado ocorre durante uma atualização, quando não há espaço suficiente para armazenar a nova linha no local original.)|
|**Linhas fantasmas**|O número de linhas que estão marcadas como excluídas, mas ainda não foram removidas. Essas linhas serão removidas por um thread de limpeza, quando o servidor não estiver ocupado. Esse valor não inclui linhas que estejam sendo retidas devido a uma transação de isolamento de instantâneo pendente.|
|**Tipo de índice**|O tipo do índice. Os valores possíveis são **Índice cluster**, **Índice não cluster**e **XML Primário**. As tabelas também podem ser armazenadas como um heap (sem-índices), mas nesse caso a página Propriedades do Índice não pode ser aberta.|
|**Linhas em nível folha**|O número de linhas em nível folha.|
|**Tamanho máximo da linha**|O tamanho máximo da linha em nível folha.|
|**Tamanho mínimo da linha**|O tamanho mínimo da linha em nível folha.|
|**Páginas**|O número total de páginas de dados.|
|**Identificação da Partição**|A ID da partição da árvore b que contém o índice.|
|**Linhas fantasmas de versão**|O número de registros fantasmas que estão sendo retidos devido a uma transação de isolamento de instantâneo pendente.|

## <a name="TsqlProcedureFrag"></a> Verificar a fragmentação de índice usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]

### <a name="to-check-the-fragmentation-of-a-rowstore-index"></a>Para verificar a fragmentação de um índice de rowstore

O exemplo a seguir localiza a porcentagem de fragmentação média de todos os índices na tabela `HumanResources.Employee` no banco de dados `AdventureWorks2016`.

```sql
SELECT a.object_id, object_name(a.object_id) AS TableName,
    a.index_id, name AS IndedxName, avg_fragmentation_in_percent
FROM sys.dm_db_index_physical_stats
    (DB_ID (N'AdventureWorks2016_EXT')
        , OBJECT_ID(N'HumanResources.Employee')
        , NULL
        , NULL
        , NULL) AS a
INNER JOIN sys.indexes AS b
    ON a.object_id = b.object_id
    AND a.index_id = b.index_id;
GO
```

A instrução anterior retorna um conjunto de resultados semelhante ao que segue.

```
object_id   TableName    index_id    IndexName                                             avg_fragmentation_in_percent
----------- ------------ ----------- ----------------------------------------------------- ------------------------------
1557580587  Employee     1           PK_Employee_BusinessEntityID                          0
1557580587  Employee     2           IX_Employee_OrganizationalNode                        0
1557580587  Employee     3           IX_Employee_OrganizationalLevel_OrganizationalNode    0
1557580587  Employee     5           AK_Employee_LoginID                                   66.6666666666667
1557580587  Employee     6           AK_Employee_NationalIDNumber                          50
1557580587  Employee     7           AK_Employee_rowguid                                   0

(6 row(s) affected)
```

Para saber mais, confira [sys.dm_db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).

### <a name="to-check-the-fragmentation-of-a-columnstore-index"></a>Para verificar a fragmentação de um índice de columnstore

O exemplo a seguir localiza a porcentagem de fragmentação média de todos os índices na tabela `dbo.FactResellerSalesXL_CCI` no banco de dados `AdventureWorksDW2016`.

```sql
SELECT i.object_id,
    object_name(i.object_id) AS TableName,
    i.index_id,
    i.name AS IndexName,
    100*(ISNULL(SUM(CSRowGroups.deleted_rows),0))/NULLIF(SUM(CSRowGroups.total_rows),0) AS 'Fragmentation'
FROM sys.indexes AS i  
INNER JOIN sys.dm_db_column_store_row_group_physical_stats AS CSRowGroups
    ON i.object_id = CSRowGroups.object_id
    AND i.index_id = CSRowGroups.index_id
WHERE object_name(i.object_id) = 'FactResellerSalesXL_CCI'
GROUP BY i.object_id, i.index_id, i.name
ORDER BY object_name(i.object_id), i.name;
```

A instrução anterior retorna um conjunto de resultados semelhante ao que segue.

```
object_id   TableName                   index_id    IndexName                       Fragmentation
----------- --------------------------- ----------- ------------------------------- ---------------
114099447   FactResellerSalesXL_CCI     1           IndFactResellerSalesXL_CCI      0

(1 row(s) affected)
```

## <a name="SSMSProcedureReorg"></a> Remover a fragmentação usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]

### <a name="to-reorganize-or-rebuild-an-index"></a>Para reorganizar ou recriar um índice

1. No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar um índice.
2. Expanda a pasta **Tabelas** .
3. Expanda a tabela na qual você deseja reorganizar um índice.
4. Expanda a pasta **Índices** .
5. Clique com o botão direito do mouse no índice a ser reorganizado e selecione **Reorganizar**.
6. Na caixa de diálogo **Reorganizar Índices** , verifique se o índice correto está na grade **Índices a serem reorganizados** e clique em **OK**.
7. Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.
8. Clique em **OK.**

> [!NOTE]
> A reorganização de um índice columnstore usando [!INCLUDE[ssManStudio](../../includes/ssManStudio-md.md)] combinará rowgroups `COMPRESSED`, mas não forçará a compactação de todos os rowgroup no columnstore. Os rowgroups FECHADO serão compactados, mas os rowgroups ABERTOS não serão compactados no columnstore. Para compactar todos os rowgroups, use o exemplo [!INCLUDE[tsql](../../includes/tsql-md.md)][a seguir](#TsqlProcedureReorg).

### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos os índices de uma tabela

1. No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar os índices.
2. Expanda a pasta **Tabelas** .
3. Expanda a tabela na qual você deseja reorganizar os índices.
4. Clique com o botão direito do mouse na pasta **Índices** e selecione **Reorganizar Tudo**.
5. Na caixa de diálogo **Reorganizar Índices** , verifique se os índices corretos estão na grade **Índices a serem reorganizados**e clique em OK. Para remover um índice da grade **Índices a serem reorganizados** , selecione o índice e pressione a tecla Delete.
6. Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.
7. Clique em **OK.**

### <a name="to-rebuild-an-index"></a>Para recriar um índice

1. No Pesquisador de Objetos, expanda o banco de dados que contém a tabela na qual você deseja reorganizar um índice.
2. Expanda a pasta **Tabelas** .
3. Expanda a tabela na qual você deseja reorganizar um índice.
4. Expanda a pasta **Índices** .
5. Clique com o botão direito do mouse no índice a ser reorganizado e selecione **Recompilar**.
6. Na caixa de diálogo **Recriar Índices** , verifique se o índice correto está na grade **Índices a serem recriados** e clique em **OK**.
7. Marque a caixa de seleção **Compactar dados de coluna de objeto grande** para especificar que todas as páginas que contêm dados de objeto grande (LOB) também sejam compactadas.
8. Clique em **OK.**

## <a name="TsqlProcedureReorg"></a> Remover a fragmentação usando o [!INCLUDE[tsql](../../includes/tsql-md.md)]

> [!NOTE]
> Para obter mais exemplos de como usar [!INCLUDE[tsql](../../includes/tsql-md.md)] para recompilarou reorganizar índices, CONFIRA [ exemplos de ALTER INDEX: Índices columnstore](../../t-sql/statements/alter-index-transact-sql.md#examples-columnstore-indexes) e [exemplos ALTER INDEX: Índices rowstore](../../t-sql/statements/alter-index-transact-sql.md#examples-rowstore-indexes).

### <a name="to-reorganize-a-fragmented-index"></a>Para reorganizar um índice fragmentado

O exemplo a seguir reorganiza o índice `IX_Employee_OrganizationalLevel_OrganizationalNode` na tabela `HumanResources.Employee` do banco de dados `AdventureWorks2016`.

```sql
ALTER INDEX IX_Employee_OrganizationalLevel_OrganizationalNode
    ON HumanResources.Employee
    REORGANIZE;
```

O exemplo a seguir reorganiza o índice columnstore `IndFactResellerSalesXL_CCI` na tabela `dbo.FactResellerSalesXL_CCI` do banco de dados `AdventureWorksDW2016`.

```sql
-- This command will force all CLOSED and OPEN rowgroups into the columnstore.
ALTER INDEX IndFactResellerSalesXL_CCI
    ON FactResellerSalesXL_CCI
    REORGANIZE WITH (COMPRESS_ALL_ROW_GROUPS = ON);
```

### <a name="to-reorganize-all-indexes-in-a-table"></a>Para reorganizar todos os índices de uma tabela

O exemplo a seguir reorganiza todos os índices na tabela `HumanResources.Employee` do banco de dados `AdventureWorks2016`.

```sql
ALTER INDEX ALL ON HumanResources.Employee
   REORGANIZE;
```

### <a name="to-rebuild-a-fragmented-index"></a>Para recompilar um índice fragmentado

O exemplo a seguir recompila um único índice na tabela `Employee` do banco de dados `AdventureWorks2016`.

[!code-sql[IndexDDL#AlterIndex1](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_1.sql)]

### <a name="to-rebuild-all-indexes-in-a-table"></a>Para recriar todos os índices de uma tabela

O exemplo a seguir recria todos os índices associados à tabela no banco de dados `AdventureWorks2016` usando a palavra-chave `ALL`. Três opções são especificadas.

[!code-sql[IndexDDL#AlterIndex2](../../relational-databases/indexes/codesnippet/tsql/reorganize-and-rebuild-i_2.sql)]

Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).

### <a name="automatic-index-and-statistics-management"></a>Índice automático e gerenciamento de estatísticas

Aproveite soluções como a [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag) para gerenciar automaticamente a desfragmentação de índice e as atualizações de estatísticas em um ou mais bancos de dados. Este procedimento escolhe automaticamente se deve recompilar ou reorganizar um índice de acordo com seu nível de fragmentação, entre outros parâmetros, e atualizar as estatísticas com um limite linear.

## <a name="see-also"></a>Confira também

- [Guia de arquitetura e design de índices do SQL Server](../../relational-databases/sql-server-index-design-guide.md)
- [Executar operações de índice online](../../relational-databases/indexes/perform-index-operations-online.md)
- [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)
- [Desfragmentação de índice adaptável](https://github.com/Microsoft/tigertoolbox/tree/master/AdaptiveIndexDefrag)
- [CREATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/create-statistics-transact-sql.md)
- [UPDATE STATISTICS &#40;Transact-SQL&#41;](../../t-sql/statements/update-statistics-transact-sql.md)
- [Desempenho de consultas de índices columnstore](../../relational-databases/indexes/columnstore-indexes-query-performance.md)
- [Introdução ao Columnstore para análise operacional em tempo real](../../relational-databases/indexes/get-started-with-columnstore-for-real-time-operational-analytics.md)
- [Índices columnstore para Data Warehousing](../../relational-databases/indexes/columnstore-indexes-data-warehouse.md)
- [Columnstore indexes and the merge policy for rowgroups (Índices columnstore e a política de mesclagem para rowgroups)](https://blogs.msdn.microsoft.com/sqlserverstorageengine/2016/03/08/columnstore-index-merge-policy-for-reorganize/)
