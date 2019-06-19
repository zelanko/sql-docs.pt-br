---
title: Usando índices Columnstore clusterizados | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: 5af6b91c-724f-45ac-aff1-7555014914f4
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 1e65c3e277eb9a3e5e3703525b9c1ac06b423c96
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62773729"
---
# <a name="using-clustered-columnstore-indexes"></a>Usando índices columnstore clusterizados
  Tarefas para usar índices columnstore clusterizados no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Para obter uma visão geral de índices columnstore, consulte [Columnstore Indexes Described](../relational-databases/indexes/columnstore-indexes-described.md).  
  
 Para obter informações sobre índices columnstore clusterizados, consulte [Using Clustered Columnstore Indexes](../relational-databases/indexes/indexes.md).  
  
## <a name="contents"></a>Sumário  
  
-   [Criar um índice Columnstore clusterizado](#create)  
  
-   [Descartar um índice Columnstore clusterizado](#drop)  
  
-   [Carregar dados em um índice Columnstore clusterizado](#load)  
  
-   [Alterar dados em um índice Columnstore clusterizado](#change)  
  
-   [Recompilar um índice Columnstore clusterizado](#rebuild)  
  
-   [Reorganizar um índice Columnstore clusterizado](#reorganize)  
  
##  <a name="create"></a> Criar um índice Columnstore clusterizado  
 Para criar um índice columnstore clusterizado, primeiro crie uma tabela rowstore como um heap ou índice clusterizado e, em seguida, use o [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) instrução para converter a tabela em um cluster índice ColumnStore. Se você desejar que o índice columnstore clusterizado tenha o mesmo nome que o índice clusterizado, use a opção DROP_EXISTING.  
  
 Este exemplo cria uma tabela como um heap e, depois, converte-o em um índice columnstore clusterizado chamado o cci_Simple. Isso altera o armazenamento da tabela inteira, de rowstore a columnstore.  
  
```  
CREATE TABLE T1(  
    ProductKey [int] NOT NULL,   
    OrderDateKey [int] NOT NULL,   
    DueDateKey [int] NOT NULL,   
    ShipDateKey [int] NOT NULL);  
GO  
CREATE CLUSTERED COLUMNSTORE INDEX cci_T1 ON T1;  
GO  
```  
  
 Para obter mais exemplos, consulte a seção de exemplos na [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-columnstore-index-transact-sql).  
  
##  <a name="drop"></a> Descartar um índice Columnstore clusterizado  
 Use o [DROP INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/drop-index-transact-sql) instrução para descartar um índice columnstore clusterizado. Essa operação irá remover o índice e converter a tabela columnstore em um heap rowstore.  
  
##  <a name="load"></a> Carregar dados em um índice Columnstore clusterizado  
 Você pode adicionar dados a um índice columnstore clusterizado existente usando qualquer um dos métodos de carregamento padrão.  Por exemplo, a carregamento em massa bcp ferramenta, Integration Services e INSERT... SELECT pode carregar todos os dados em um índice columnstore clusterizado.  
  
 Os índices columnstore clusterizados aproveitam o deltastore a fim de evitar a fragmentação de segmentos de colunas no columnstore.  
  
### <a name="loading-into-a-partitioned-table"></a>Carregando em uma tabela particionada  
 Para dados particionados, primeiro o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atribui cada linha a uma partição e, depois, executa operações columnstore nos dados na partição. Cada partição tem seus próprios rowgroups e pelo menos um deltastore.  
  
### <a name="deltastore-loading-scenarios"></a>Cenários de carregamento de deltastore  
 As linhas são acumuladas no deltastore até que o número de linhas atinja o número máximo de linhas permitido para um rowgroup. Quando o deltastore contiver o número máximo de linhas por rowgroup, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marcará o rowgroup como "CLOSED". Um processo em segundo plano, chamado "motor de tupla", localiza o rowgroup CLOSED e move para o columnstore, onde o rowgroup é compactado em segmentos de coluna e os segmentos de coluna são armazenados no columnstore.  
  
 Para cada índice columnstore clusterizado, podem existir vários deltastores.  
  
-   Se um deltastore estiver bloqueado, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tentará obter um bloqueio em outro deltastore. Se não houver nenhum deltastore disponível, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] criará um novo deltastore.  
  
-   Para uma tabela particionada, podem existir um ou mais deltastores para cada partição.  
  
 Para apenas índices columnstore clusterizados, os cenários a seguir descrevem quando as linhas carregadas vão diretamente para o columnstore, ou quando elas vão para o deltastore.  
  
 No exemplo, cada rowgroup pode ter de 102.400 a 1.048.576 linhas por rowgroup.  
  
|Linhas para carregamento em massa|Linhas adicionadas ao columnstore|Linhas adicionadas ao deltastore|  
|-----------------------|-----------------------------------|----------------------------------|  
|102.000|0|102.000|  
|145.000|145.000<br /><br /> Tamanho do rowgroup: 145.000|0|  
|1,048,577|1\.048.576<br /><br /> Tamanho do rowgroup: 1.048.576.|1|  
|2,252,152|2,252,152<br /><br /> Tamanhos dos rowgroups: 1.048.576, 1.048.576, 155.000.|0|  
  
 O exemplo a seguir mostra os resultados do carregamento de 1.048.577 linhas em uma partição. Os resultados mostram um rowgroup COMPRESSED no columnstore (como segmentos de coluna compactados) e 1 linha no deltastore.  
  
```  
SELECT * FROM sys.column_store_row_groups  
```  
  
 ![Rowgroup e deltastore para uma carga em lote](../../2014/database-engine/media/sql-server-pdw-columnstore-batchload.gif "Rowgroup e deltastore para uma carga em lote")  
  

  
##  <a name="change"></a> Alterar dados em um índice Columnstore clusterizado  
 Os índices columnstore clusterizados oferecem suporte a operações DML de inserção, atualização e exclusão.  
  
 Use [INSERT &#40;Transact-SQL&#41; ](/sql/t-sql/statements/insert-transact-sql) para inserir uma linha. A linha será adicionada ao deltastore.  
  
 Use [DELETE &#40;Transact-SQL&#41;](/sql/t-sql/statements/delete-transact-sql) para excluir uma linha.  
  
-   Se a linha estiver no columnstore, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marcará a linha como excluída logicamente, mas não recuperará o armazenamento físico da linha até que o índice seja recriado.  
  
-   Se a linha estiver no deltastore, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] excluirá a linha lógica e fisicamente.  
  
 Use [UPDATE &#40;Transact-SQL&#41;](/sql/t-sql/queries/update-transact-sql) para atualizar uma linha.  
  
-   Se a linha estiver no columnstore, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] marcará a linha como excluída logicamente e irá inserir a linha atualizada no deltastore.  
  
-   Se a linha estiver no deltastore, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] atualizará a linha no deltastore.  
  
##  <a name="rebuild"></a> Recompilar um índice Columnstore clusterizado  
 Use [CREATE CLUSTERED COLUMNSTORE INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/create-columnstore-index-transact-sql) ou [ALTER INDEX &#40;Transact-SQL&#41; ](/sql/t-sql/statements/alter-index-transact-sql) para executar uma recriação completa de um índice columnstore clusterizado existente. Além disso, você pode usar ALTER INDEX ... REBUILD para recompilar uma partição específica.  
  
### <a name="rebuild-process"></a>Processo de recriação  
 Para recompilar um índice columnstore clusterizado, [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]:  
  
-   Obtenha um bloqueio exclusivo na tabela ou na partição durante a recompilação.  Os dados ficam "offline" e não disponíveis enquanto você recompila.  
  
-   Desfragmenta o columnstore excluindo fisicamente as linhas que foram excluídas logicamente da tabela; os bytes excluídos são recuperados na mídia física.  
  
-   Mescla os dados do rowstore no deltastore com os dados do columnstore antes da recriação do índice. Quando a recriação é concluída, todos os dados são armazenados no formato columnstore, e o deltastore está vazio.  
  
-   Compacta novamente todos os dados do columnstore. Há duas cópias do índice columnstore durante a recompilação. Quando a recompilação é concluída, o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] exclui o índice columnstore original.  
  
### <a name="recommendations-for-rebuilding-a-clustered-columnstore-index"></a>Recomendações para recriar um índice columnstore clusterizado  
 Recriar um índice columnstore clusterizado é útil para remover a fragmentação, e para mover todas as linhas para o columnstore. Nossas recomendações:  
  
-   Recriar uma partição em vez de toda a tabela.  
  
    1.  Recriar a tabela inteira é uma tarefa demorada se o índice é grande, e isso exige espaço em disco suficiente para armazenar uma cópia adicional do índice durante a recriação. Geralmente, é necessário recriar apenas a partição mais recentemente usada.  
  
    2.  Em tabelas particionadas, não é necessário recriar todo o índice columnstore, pois é provável que a fragmentação ocorra apenas nas partições que foram modificadas recentemente. As tabelas de fatos e de dimensões grandes geralmente são particionadas para executar operações de backup e gerenciamento em partes da tabela.  
  
-   Recriar uma partição após operações DML pesadas.  
  
     Recriar uma partição desfragmentará a partição e reduzirá o armazenamento em disco. Essa recriação excluirá todas as linhas do columnstore que são marcadas para exclusão, e moverá todas as linhas do deltastore para o columnstore.  
  
-   Recriar uma partição após carregar dados.  
  
     Isso garante que todos dados sejam armazenados no columnstore. Se vários carregamentos ocorrerem ao mesmo tempo, cada partição poderá acabar tendo vários deltastores. A recriação moverá todas as linhas do deltastore para o columnstore.  
  
##  <a name="reorganize"></a> Reorganizar um índice Columnstore clusterizado  
 A reorganização de um índice columnstore clusterizado move todos os rowgroups CLOSED para o columnstore. Para executar uma reorganização, use [ALTER INDEX &#40;Transact-SQL&#41;](/sql/t-sql/statements/alter-index-transact-sql)com a opção REORGANIZE.  
  
 A reorganização não é necessária para mover rowgroups CLOSED para o columnstore. O processo Tuple Mover acabará encontrando todos os rowgroups FECHADOS e os moverá. No entanto, o Tuple Mover tem thread único e não pode mover rowgroups com rapidez suficiente para a carga de trabalho.  
  
### <a name="recommendations-for-reorganizing"></a>Recomendações para reorganizar  
 Quando reorganizar um índice columnstore clusterizado:  
  
-   Reorganize um índice columnstore clusterizado depois que um ou mais carregamentos de dados atingir os benefícios de desempenho de consulta o mais rapidamente possível. Inicialmente, a reorganização exigirá recursos de CPU adicionais para compactar os dados, o que pode reduzir o desempenho geral do sistema. No entanto, assim que os dados forem compactados, o desempenho de consulta poderá aumentar.  
  
  
