---
title: DBCC SHOWCONTIG (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/17/2017
ms.prod: sql
ms.prod_service: sql-database
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DBCC_SHOWCONTIG_TSQL
- DBCC SHOWCONTIG
- SHOWCONTIG
- SHOWCONTIG_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- displaying defragmentation information
- DBCC SHOWCONTIG statement
- defragmenting indexes
- leaf level defragmenting
- fragmentation [SQL Server]
- index defragmenting [SQL Server]
ms.assetid: 1df2123a-1197-4fff-91a3-25e3d8848aaa
author: pmasl
ms.author: umajay
ms.openlocfilehash: 3e177015f1d17ff28fe702a4c5998f97999b66ec
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882027"
---
# <a name="dbcc-showcontig-transact-sql"></a>DBCC SHOWCONTIG (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

Exibe informações de fragmentação para os dados e índices da tabela ou exibição especificada.
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureDontUse](../../includes/ssnotedepfuturedontuse-md.md)] Use [db_index_physical_stats](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md) nesse caso.  
  
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](https://go.microsoft.com/fwlink/p/?LinkId=299658))
  
![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DBCC SHOWCONTIG   
[ (   
    { table_name | table_id | view_name | view_id }   
    [ , index_name | index_id ]   
) ]   
    [ WITH   
        {   
         [ , [ ALL_INDEXES ] ]   
         [ , [ TABLERESULTS ] ]   
         [ , [ FAST ] ]  
         [ , [ ALL_LEVELS ] ]   
         [ NO_INFOMSGS ]  
         }  
    ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *table_name* | *table_id* | *view_name* | *view_id*  
 É a tabela ou exibição de verificação das informações de fragmentação. Se não for especificado, serão verificadas todas as tabelas e exibições indexadas no banco de dados atual. Para obter a tabela ou exibir a ID, use a função [OBJECT_ID](../../t-sql/functions/object-id-transact-sql.md).  
  
 *index_name* | *index_id*  
 É o índice de verificação das informações de fragmentação. Se não for especificado, a instrução processará o índice base da tabela ou exibição especificada. Para obter a ID de índice, use a exibição de catálogo [sys.indexes](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md).  
  
 WITH  
 Especifica opções para o tipo de informações retornado pela instrução DBCC.  
  
 FAST  
 Especifica se deve ser executada uma verificação rápida das informações mínimas de índice e de saída. Uma verificação rápida não lê as páginas em nível de dados ou folha do índice.  
  
 ALL_INDEXES  
 Exibe resultados para todos os índices das tabelas e exibições especificadas, até mesmo se um índice particular for especificado.  
  
 TABLERESULTS  
 Exibe resultados como um conjunto de linhas, com informações adicionais.  
  
 ALL_LEVELS  
 Mantido somente para compatibilidade com versões anteriores. Mesmo se ALL_LEVELS for especificado, só o nível folha de índice ou o nível de dados de tabela será processado.  
  
 NO_INFOMSGS  
 Suprime todas as mensagens informativas com níveis de severidade de 0 a 10.  
  
## <a name="result-sets"></a>Conjuntos de resultados  
A tabela a seguir descreve as informações do conjunto de resultados.
  
|Estatística|Descrição|  
|---|---|
|**Páginas verificadas**|Número de páginas na tabela ou no índice.|  
|**Extensões verificadas**|Número de extensões na tabela ou no índice.|  
|**Opções de extensão**|O número de vezes que a instrução DBCC foi movida de uma extensão para outra enquanto atravessava as páginas da tabela ou do índice.|  
|**Méd. de Páginas por extensão**|Número de páginas por extensão na cadeia de páginas.|  
|**Densidade da verificação [melhor contagem: contagem real]**|É uma porcentagem. É a taxa de **Melhor Contagem** para **Contagem Real**. Esse valor será 100 se tudo for contíguo; se ele for menor que 100, isso indicará que existe alguma fragmentação.<br /><br /> **Melhor Contagem** será o número ideal de alterações de extensão se tudo estiver vinculado de forma contígua. **Contagem Real** é o número real de alterações de extensão.|  
|**Fragmentação da verificação lógica**|Porcentagem de páginas com problema retornadas da verificação de páginas de folha de um índice. Esse número não é relevante para heaps. Uma página fora de ordem é aquela cuja próxima página física alocada ao índice não é a página apontada pelo ponteiro de próxima págin*a* na página de folha atual.|  
|**Fragmentação da verificação de extensão**|Porcentagem de extensões com problemas na verificação de páginas de folha de um índice. Esse número não é relevante para heaps. Uma extensão com problema é aquela para a qual a extensão que contém a página atual de um índice não é fisicamente a próxima extensão depois da extensão que contém a página anterior de um índice.<br /><br /> Observação: Esse número não tem sentido quando o índice se estende a vários arquivos.|  
|**Méd. de Bytes livres por página**|Número médio de bytes livres em páginas verificadas. Quanto maior o número, mais vazias ficarão as páginas. Números inferiores serão melhores se o índice não tiver muitas inserções aleatórias. Esse número também é afetado pelo tamanho da linha; uma linha grande pode gerar um número maior.|  
|**Méd. de Densidade de página (completa)**|Densidade média da página, como uma porcentagem. Esse valor leva em consideração o tamanho de linha. Por isso, o valor é uma indicação mais precisa de quão cheias estão as páginas. Quanto maior a porcentagem, melhor.|  
  
Quando *table_id* e FAST forem especificados, DBCC SHOWCONTIG retornará um conjunto de resultados apenas com as próximas colunas.
-   **Páginas verificadas**  
-   **Opções de extensão**  
-   **Densidade da verificação [melhor contagem : contagem real]**  
-   **Fragmentação da verificação de extensão**  
-   **Fragmentação da verificação lógica**  
  
Quando TABLERESULTS é especificado, DBCC SHOWCONTIG retorna as seguintes colunas e também as nove colunas descritas na tabela anterior.
  
|Estatística|Descrição|  
|---|---|
|**Object Name**|Nome da tabela ou exibição processada.|  
|**ObjectId**|ID do nome do objeto.|  
|**IndexName**|Nome do índice processado. É NULL para um heap.|  
|**IndexId**|ID do índice. É 0 para um heap.|  
|**Level**|Nível do índice. Nível 0 é o nível folha ou dados do índice.<br /><br /> Nível é 0 para um heap.|  
|**Páginas**|Número de páginas que compõem o nível do índice ou de todo o heap.|  
|**Linhas**|Número de dados ou registros de índice no nível do índice. Para um heap, esse valor é o número de registros de dados em todo o heap.<br /><br /> Para um heap, o número de registros retornados de sua função pode não corresponder ao número de linhas retornadas devido à execução de SELECT COUNT(*) relacionada ao heap. Isso porque uma linha pode conter vários registros. Por exemplo, em algumas situações de atualização, uma única linha de heap pode ter um registro de encaminhamento e um registro encaminhado como resultado de uma operação de atualização. Da mesma forma, a maior parte das linhas de LOB grandes é dividida em vários registros no armazenamento LOB_DATA.|  
|**MinimumRecordSize**|Tamanho mínimo do registro no nível do índice ou de todo o heap.|  
|**MaximumRecordSize**|Tamanho máximo do registro no nível do índice ou de todo o heap.|  
|**AverageRecordSize**|Tamanho médio do registro no nível do índice ou de todo o heap.|  
|**ForwardedRecords**|Número de registros encaminhados no nível do índice ou de todo o heap.|  
|**Extensões**|Número de extensões no nível do índice ou de todo o heap.|  
|**ExtentSwitches**|O número de vezes que a instrução DBCC foi movida de uma extensão para outra enquanto atravessava as páginas da tabela ou do índice.|  
|**AverageFreeBytes**|Número médio de bytes livres em páginas verificadas. Quanto maior o número, mais vazias ficarão as páginas. Números inferiores serão melhores se o índice não tiver muitas inserções aleatórias. Esse número também é afetado pelo tamanho da linha; uma linha grande pode gerar um número maior.|  
|**AveragePageDensity**|Densidade média da página, como uma porcentagem. Esse valor leva em consideração o tamanho de linha. Por isso, o valor é uma indicação mais precisa de quão cheias estão as páginas. Quanto maior a porcentagem, melhor.|  
|**ScanDensity**|É uma porcentagem. É a taxa de **BestCount** para **ActualCount**. Esse valor será 100 se tudo for contíguo; se ele for menor que 100, isso indicará que existe alguma fragmentação.|  
|**BestCount**|Será o número ideal de alterações de extensão se tudo for vinculado contiguamente.|  
|**ActualCount**|É o número real de alterações de extensão.|  
|**LogicalFragmentation**|Porcentagem de páginas com problema retornadas da verificação de páginas de folha de um índice. Esse número não é relevante para heaps. Uma página fora de ordem é aquela cuja próxima página física alocada ao índice não é a página apontada pelo ponteiro de próxima págin*a* na página de folha atual.|  
|**ExtentFragmentation**|Porcentagem de extensões com problemas na verificação de páginas de folha de um índice. Esse número não é relevante para heaps. Uma extensão com problema é aquela para a qual a extensão que contém a página atual de um índice não é fisicamente a próxima extensão depois da extensão que contém a página anterior de um índice.<br /><br /> Observação: Esse número não tem sentido quando o índice se estende a vários arquivos.|  
  
Quando WITH TABLERESULTS e FAST forem especificados, o conjunto de resultados será o mesmo de quando WITH TABLERESULTS for especificado, exceto que as seguintes colunas terão valores nulos:

| Linhas| Extensões |
|---|---|
|**MinimumRecordSize**|**AverageFreeBytes**|  
|**MaximumRecordSize**|**AveragePageDensity**|  
|**AverageRecordSize**|**ExtentFragmentation**|  
|**ForwardedRecords**||  
  
## <a name="remarks"></a>Comentários  
A instrução DBCC SHOWCONTIG atravessa a cadeia de páginas no nível da folha do índice especificado quando *index_id* é especificado. Se apenas *table_id* for especificado ou se *index_id* for 0, as páginas de dados da tabela especificada serão verificadas. A operação somente requer um bloqueio de tabela de tentativa compartilhada (IS). Desse modo, podem ser executadas todas as atualizações e inserções, exceto as que exigirem um bloqueio de tabela exclusivo (X). Isso permite um equilíbrio entre a velocidade da execução e nenhuma redução da simultaneidade em relação ao número de estatísticas retornadas. Entretanto, se o comando estiver sendo usado apenas para medir a fragmentação, recomendamos o uso da opção WITH FAST para obter um desempenho melhor. Uma verificação rápida não lê as páginas em nível de dados ou folha do índice. A opção WITH FAST não se aplica a um heap.
  
## <a name="restrictions"></a>Restrições  
DBCC SHOWCONTIG não exibe dados com os tipos de dados **ntext**, **text** e **image**. Isso ocorre porque os índices de texto que armazenam dados de texto e imagem já não existem mais.
  
Da mesma forma, DBCC SHOWCONTIG não oferece suporte a alguns recursos novos. Por exemplo:
-   Se a tabela ou o índice especificado for particionado, DBCC SHOWCONTIG exibirá apenas a primeira partição da tabela ou índice especificado.  
-   DBCC SHOWCONTIG não exibe informações de armazenamento de estouro de linha e de outros novos tipos de dados fora da linha, como **nvarchar(max)** , **varchar(max)** , **varbinary(max)** e **XML**.  
-   Não há suporte para índices de espaço pelo DBCC SHOWCONTIG.  
  
Todos os novos recursos são totalmente compatíveis com a exibição de gerenciamento dinâmico [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md).
  
## <a name="table-fragmentation"></a>Fragmentação de tabela  
DBCC SHOWCONTIG determina se a tabela está muito fragmentada. A fragmentação da tabela ocorre pelo processo de modificações de dados (instruções INSERT, UPDATE e DELETE) efetuado na tabela. Como essas modificações não são distribuídas uniformemente entre as linhas da tabela, o preenchimento de cada página pode variar com o tempo. Para consultas que verificam parte de uma tabela ou toda ela, tal fragmentação de tabela pode causar leituras de página adicionais. Isso impede o exame paralelo de dados.
  
Quando um índice está bastante fragmentado, as opções a seguir são disponibilizadas para reduzir a fragmentação:
-   Descartar e recriar um índice clusterizado.  
     Recriar um índice clusterizado reorganiza os dados e gera páginas de dados cheias. O nível de preenchimento pode ser configurado usando a opção FILLFACTOR em CREATE INDEX. As desvantagens desse método são que o índice fica offline durante o ciclo de descarte ou recriação e que a operação é atômica. Se a criação de índice for suspensa, o índice não será recriado.  
-   Reordenar as páginas de nível folha do índice em uma ordem lógica.  
     Use ALTER INDEX...REORGANIZE para reordenar as páginas no nível da folha do índice em uma ordem lógica. Por essa operação ser online, o índice estará disponível quando a instrução estiver em execução. A operação também pode ser interrompida sem perda de trabalho concluído. A desvantagem desse método é que ele não reorganiza muito bem os dados como uma operação de recriação ou descarte de índice clusterizado.  
-   Reconstruir o índice.  
     Use ALTER INDEX com REBUILD para reconstruir o índice. Para obter mais informações, consulte [ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md).  
  
O número da **Média de bytes livres por página** e **Média de densidade de página (completa)** no conjunto de resultados indicam o preenchimento de páginas de índice. O número da **Média de bytes livres por página** deve ser baixo e o número da **Média de densidade de página (completa)** deve ser alto para um índice sem muitas inserções aleatórias. Descartar e recriar um índice com a opção de FILLFACTOR especificada pode melhorar as estatísticas. Da mesma forma, ALTER INDEX com REORGANIZE compactará um índice, levando em conta seu FILLFACTOR e melhorará as estatísticas.
  
> [!NOTE]  
>  Um índice que tem muitas inserções aleatórias e páginas muito cheias terá um número maior de separações de página. Isso causa mais fragmentação.  
  
O nível de fragmentação de um índice pode ser determinado dos seguintes modos:
-   Comparando os valores de **Opções de extensão** e **Extensões verificadas**.  
     O valor de **Opções de extensão** deve ser o mais próximo possível do valor de **Extensões verificadas**. Essa taxa é calculada como o valor de **Densidade da Verificação**. Esse valor deve ser o mais alto possível e pode ser melhorado reduzindo-se a fragmentação de índice.  
  
    > [!NOTE]  
    >  Esse método não funcionará se o índice se estender a vários arquivos.  
  
-   Entendendo os valores de **Fragmentação da Verificação Lógica** e de **Fragmentação da Verificação de Extensão**.  
     Os valores de **Fragmentação da Verificação Lógica** e, em um âmbito menor, **Fragmentação da Verificação de Extensão** são os melhores indicadores do nível de fragmentação de uma tabela. Esses dois valores devem ser o mais próximo possível de zero, embora um valor de 0 a 10% possa ser aceito.  
  
    > [!NOTE]  
    >  O valor de **Fragmentação da Verificação de Extensão** será alto se o índice abranger vários arquivos. Para reduzir esses valores, você deve reduzir a fragmentação de índice.  
  
## <a name="permissions"></a>Permissões  
O usuário precisa ser o proprietário da tabela ou ser membro da função de servidor fixa **sysadmin**, da função de banco de dados fixa **db_owner** ou da função de banco de dados fixa **db_ddladmin**.
  
## <a name="examples"></a>Exemplos  
### <a name="a-displaying-fragmentation-information-for-a-table"></a>a. Exibindo informações de fragmentação de uma tabela  
O exemplo a seguir exibe informações de fragmentação da tabela `Employee`.
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('HumanResources.Employee');  
GO  
```  
  
### <a name="b-using-object_id-to-obtain-the-table-id-and-sysindexes-to-obtain-the-index-id"></a>B. Usando OBJECT_ID para obter a ID de tabela e sys.indexes para obter a ID de índice  
O exemplo a seguir usa `OBJECT_ID` e a exibição de catálogo `sys.indexes` para obter a ID da tabela e a ID do índice para o índice `AK_Product_Name` da tabela `Production.Product` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
USE AdventureWorks2012;  
GO  
DECLARE @id int, @indid int  
SET @id = OBJECT_ID('Production.Product')  
SELECT @indid = index_id   
FROM sys.indexes  
WHERE object_id = @id   
   AND name = 'AK_Product_Name'  
DBCC SHOWCONTIG (@id, @indid);  
GO  
```  
  
### <a name="c-displaying-an-abbreviated-result-set-for-a-table"></a>C. Exibindo um conjunto de resultados abreviado para uma tabela  
O exemplo a seguir retorna um conjunto de resultados abreviado para a tabela `Product` no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG ('Production.Product', 1) WITH FAST;  
GO  
```  
  
### <a name="d-displaying-the-full-result-set-for-every-index-on-every-table-in-a-database"></a>D. Exibindo o conjunto de resultados completo de todos os índices de todas as tabelas em um banco de dados  
O exemplo a seguir retorna um conjunto de resultados de tabela completo de todos os índices em todas as tabelas no banco de dados [!INCLUDE[ssSampleDBobject](../../includes/sssampledbobject-md.md)].
  
```sql  
USE AdventureWorks2012;  
GO  
DBCC SHOWCONTIG WITH TABLERESULTS, ALL_INDEXES;  
GO  
```  
  
### <a name="e-using-dbcc-showcontig-and-dbcc-indexdefrag-to-defragment-the-indexes-in-a-database"></a>E. Usando DBCC SHOWCONTIG e DBCC INDEXDEFRAG para desfragmentar os índices em um banco de dados  
O exemplo a seguir mostra uma maneira simples de desfragmentar todos os índices em um banco de dados que estão fragmentados acima de um limite declarado.
  
```sql
/*Perform a 'USE <database name>' to select the database in which to run the script.*/  
-- Declare variables  
SET NOCOUNT ON;  
DECLARE @tablename varchar(255);  
DECLARE @execstr   varchar(400);  
DECLARE @objectid  int;  
DECLARE @indexid   int;  
DECLARE @frag      decimal;  
DECLARE @maxfrag   decimal;  
  
-- Decide on the maximum fragmentation to allow for.  
SELECT @maxfrag = 30.0;  
  
-- Declare a cursor.  
DECLARE tables CURSOR FOR  
   SELECT TABLE_SCHEMA + '.' + TABLE_NAME  
   FROM INFORMATION_SCHEMA.TABLES  
   WHERE TABLE_TYPE = 'BASE TABLE';  
  
-- Create the table.  
CREATE TABLE #fraglist (  
   ObjectName char(255),  
   ObjectId int,  
   IndexName char(255),  
   IndexId int,  
   Lvl int,  
   CountPages int,  
   CountRows int,  
   MinRecSize int,  
   MaxRecSize int,  
   AvgRecSize int,  
   ForRecCount int,  
   Extents int,  
   ExtentSwitches int,  
   AvgFreeBytes int,  
   AvgPageDensity int,  
   ScanDensity decimal,  
   BestCount int,  
   ActualCount int,  
   LogicalFrag decimal,  
   ExtentFrag decimal);  
  
-- Open the cursor.  
OPEN tables;  
  
-- Loop through all the tables in the database.  
FETCH NEXT  
   FROM tables  
   INTO @tablename;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
-- Do the showcontig of all indexes of the table  
   INSERT INTO #fraglist   
   EXEC ('DBCC SHOWCONTIG (''' + @tablename + ''')   
      WITH FAST, TABLERESULTS, ALL_INDEXES, NO_INFOMSGS');  
   FETCH NEXT  
      FROM tables  
      INTO @tablename;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE tables;  
DEALLOCATE tables;  
  
-- Declare the cursor for the list of indexes to be defragged.  
DECLARE indexes CURSOR FOR  
   SELECT ObjectName, ObjectId, IndexId, LogicalFrag  
   FROM #fraglist  
   WHERE LogicalFrag >= @maxfrag  
      AND INDEXPROPERTY (ObjectId, IndexName, 'IndexDepth') > 0;  
  
-- Open the cursor.  
OPEN indexes;  
  
-- Loop through the indexes.  
FETCH NEXT  
   FROM indexes  
   INTO @tablename, @objectid, @indexid, @frag;  
  
WHILE @@FETCH_STATUS = 0  
BEGIN  
   PRINT 'Executing DBCC INDEXDEFRAG (0, ' + RTRIM(@tablename) + ',  
      ' + RTRIM(@indexid) + ') - fragmentation currently '  
       + RTRIM(CONVERT(varchar(15),@frag)) + '%';  
   SELECT @execstr = 'DBCC INDEXDEFRAG (0, ' + RTRIM(@objectid) + ',  
       ' + RTRIM(@indexid) + ')';  
   EXEC (@execstr);  
  
   FETCH NEXT  
      FROM indexes  
      INTO @tablename, @objectid, @indexid, @frag;  
END;  
  
-- Close and deallocate the cursor.  
CLOSE indexes;  
DEALLOCATE indexes;  
  
-- Delete the temporary table.  
DROP TABLE #fraglist;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[ALTER INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-index-transact-sql.md)  
[CREATE INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-index-transact-sql.md)  
[DBCC &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-transact-sql.md)  
[DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md)  
[sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
[OBJECT_ID &#40;Transact-SQL&#41;](../../t-sql/functions/object-id-transact-sql.md)  
[sys.indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-indexes-transact-sql.md)
  
  

