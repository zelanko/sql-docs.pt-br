---
title: Gerenciar índices de texto completo | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-search
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 28ff17dc-172b-4ac4-853f-990b5dc02fd1
caps.latest.revision: 8
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 9a38476f427cbc2c9630c66020f35c5f7355e9bd
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117955"
---
# <a name="manage-full-text-indexes"></a>Gerenciar índices de texto completo
     
##  <a name="view"></a> Exibindo e alterando as propriedades de um índice de texto completo  
  
#### <a name="to-view-or-change-the-properties-of-a-full-text-index-in-management-studio"></a>Par exibir ou alterar as propriedades de um índice de texto completo no Management Studio  
  
1.  No Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e expanda o banco de dados que contém o índice de texto completo.  
  
3.  Expanda **Tabelas**.  
  
4.  Clique com o botão direito do mouse na tabela em que o índice de texto completo está definido, selecione **Índice de Texto Completo**e, no menu de contexto **Índice de Texto Completo** , clique em **Propriedades**. Este procedimento abre a caixa de diálogo **Propriedades do Índice de Texto Completo** .  
  
5.  No painel **Selecionar uma página** , você pode selecionar qualquer uma das seguintes páginas:  
  
    |Página|Description|  
    |----------|-----------------|  
    |**Geral**|Exibe as propriedades básicas do índice de texto completo. Isso inclui várias propriedades modificáveis e uma série de propriedades inalteráveis, como o nome do banco de dados, o nome da tabela e o nome da coluna de chave de texto completo. As propriedades modificáveis são:<br /><br /> **Lista de palavras irrelevantes de índice de texto completo**<br /><br /> **Indexação de texto completo habilitada**<br /><br /> **Controle de alterações**<br /><br /> **Lista de propriedades de pesquisa**<br /><br /> <br /><br /> Para obter mais informações, consulte [propriedades do índice de texto completo &#40;página geral&#41;](full-text-index-properties-general-page.md).|  
    |**Colunas**|Exibe as colunas da tabela que estão disponíveis para indexação de texto completo. A(s) coluna(s) selecionada(s) tem(têm) índice de texto completo. Você pode selecionar tantas colunas disponíveis quantas desejar para incluí-las no índice de texto completo. Para obter mais informações, consulte [propriedades do índice de texto completo &#40;página colunas&#41;](../../2014/database-engine/full-text-index-properties-columns-page.md).|  
    |**Agendas**|Use esta página para criar ou gerenciar agendas para executar um trabalho do SQL Server Agent que inicia uma população incremental de tabela para as populações de índice de texto completo. Para obter mais informações, veja [Popular índices de texto completo](../relational-databases/indexes/indexes.md).<br /><br /> **\*\* Importante \* \***  depois que você sair do **propriedades do índice de texto completo** caixa de diálogo, qualquer agenda recém-criada será associada um trabalho do SQL Server Agent (Iniciar população Incremental da tabela em *database_name*. *table_name*).|  
  
6.  [!INCLUDE[clickOK](../includes/clickok-md.md)] para salvar quaisquer alterações e sair da caixa de diálogo **Propriedades do índice de texto completo**.  
  
##  <a name="props"></a> Exibindo as propriedades de colunas e tabelas indexadas  
 Muitas funções [!INCLUDE[tsql](../includes/tsql-md.md)], como OBJECTPROPERTYEX, podem ser usadas para obter o valor de diversas propriedades de indexação de texto completo. Essas informações são úteis para administrar e solucionar problemas de pesquisa de texto completo.  
  
 A tabela a seguir lista as propriedades de texto completo relacionadas a colunas e tabelas indexadas e suas funções [!INCLUDE[tsql](../includes/tsql-md.md)] relacionadas.  
  
|Propriedade|Description|Função|  
|--------------|-----------------|--------------|  
|`FullTextTypeColumn`|TYPE COLUMN na tabela que armazena as informações de tipo de documento da coluna.|[COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql)|  
|`IsFulltextIndexed`|Se uma coluna foi habilitada para indexação de texto completo.|COLUMNPROPERTY|  
|`IsFulltextKey`|Se o índice é a chave de texto completo de uma tabela.|[INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql)|  
|**TableFulltextBackgroundUpdateIndexOn**|Se uma tabela tem indexação de atualização de texto completo em segundo plano.|[OBJECTPROPERTYEX](/sql/t-sql/functions/objectproperty-transact-sql)|  
|`TableFulltextCatalogId`|ID do catálogo de texto completo no qual residem os dados de índice de texto completo da tabela.|OBJECTPROPERTYEX|  
|`TableFulltextChangeTrackingOn`|Se o controle de alterações de texto completo está habilitado em uma tabela.|OBJECTPROPERTYEX|  
|`TableFulltextDocsProcessed`|Número de linhas processadas desde o início da indexação de texto completo.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|Número de linhas que a Pesquisa de Texto Completo não indexou.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|Número de linhas que foram indexadas com texto completo com êxito.|OBJECTPROPERTYEX|  
|`TableFulltextKeyColumn`|A ID de coluna da coluna de chave exclusiva de texto completo.|OBJECTPROPERTYEX|  
|`TableFullTextMergeStatus`|Se uma tabela que tem um índice de texto completo está sendo mesclada.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|Número de entradas de controle de alterações pendentes a serem processadas.|OBJECTPROPERTYEX|  
|`TableFulltextPopulateStatus`|Status de população de uma tabela de texto completo.|OBJECTPROPERTYEX|  
|`TableHasActiveFulltextIndex`|Se uma tabela tem um índice de texto completo ativo.|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> Obtendo informações sobre a coluna de chave de texto completo  
 Normalmente, o resultado de funções com valor de conjunto de linhas CONTAINSTABLE ou FREETEXTTABLE precisam ser unidas à tabela base. Nesses casos, você precisa saber o nome da coluna de chave exclusiva. Você pode perguntar se um dado índice exclusivo é usado como chave de texto completo e pode obter o identificador da coluna de chave de texto completo.  
  
#### <a name="to-inquire-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>Para perguntar se um dado índice de texto completo é usado como a coluna de chave de texto completo  
  
1.  Use uma instrução [SELECT](/sql/t-sql/queries/select-transact-sql) para chamar a função [INDEXPROPERTY](/sql/t-sql/functions/indexproperty-transact-sql). Na função de chamada, use a função OBJECT_ID para converter o nome da tabela (*table_name*) na ID de tabela, especifique o nome de um índice exclusivo para a tabela e especifique o `IsFulltextKey` propriedade de índice da seguinte maneira:  
  
    ```  
    SELECT INDEXPROPERTY( OBJECT_ID('table_name'), 'index_name',  'IsFulltextKey' );  
    ```  
  
     Esta instrução retornará 1 se o índice for usado para impor a exclusividade da coluna de chave de texto completo e 0 se o índice não for usado para realizar essa imposição.  
  
 **Exemplo**  
  
 O exemplo a seguir pergunta se o índice `PK_Document_DocumentID` é usado para impor a exclusividade da coluna de chave de texto completo, da seguinte maneira:  
  
```  
USE AdventureWorks  
GO  
SELECT INDEXPROPERTY ( OBJECT_ID('Production.Document'), 'PK_Document_DocumentID',  'IsFulltextKey' )  
```  
  
 Este exemplo retornará 1 se o índice `PK_Document_DocumentID` for usado para impor a exclusividade da coluna de chave de texto completo. Caso contrário, retornará 0 ou NULL. NULL implica que você está usando um nome de índice inválido, que o nome de índice não corresponde à tabela, que a tabela não existe, e assim por diante.  
  
#### <a name="to-find-the-identifier-of-the-full-text-key-column"></a>Para encontrar o identificador da coluna de chave de texto completo  
  
1.  Cada tabela habilitada para texto completo tem uma coluna que é usada para impor linhas exclusivas da tabela (a *coluna de chave**exclusiva*). A propriedade `TableFulltextKeyColumn`, obtida da função OBJECTPROPERTYEX, contém a ID de coluna da coluna de chave exclusiva.  
  
     Para obter esse identificador, você pode usar uma instrução SELECT para chamar a função OBJECTPROPERTYEX. Use a função OBJECT_ID para converter o nome da tabela (*table_name*) na ID de tabela e especifique o `TableFulltextKeyColumn` propriedade, da seguinte maneira:  
  
    ```  
    SELECT OBJECTPROPERTYEX(OBJECT_ID( 'table_name'), 'TableFulltextKeyColumn' ) AS 'Column Identifier';  
    ```  
  
 **Exemplos**  
  
 O próximo exemplo retorna o identificador da coluna de chave de texto completo ou NULL. NULL implica que você está usando um nome de índice inválido, que o nome de índice não corresponde à tabela, que a tabela não existe e assim por diante.  
  
```  
USE AdventureWorks;  
GO  
SELECT OBJECTPROPERTYEX(OBJECT_ID('Production.Document'), 'TableFulltextKeyColumn');  
GO  
```  
  
 O exemplo a seguir mostra como usar o identificador da coluna de chave exclusiva para obter o nome da coluna.  
  
```  
USE AdventureWorks;  
GO  
DECLARE @key_column sysname  
SET @key_column = Col_Name(Object_Id('Production.Document'),  
ObjectProperty(Object_id('Production.Document'),  
'TableFulltextKeyColumn')   
)  
SELECT @key_column AS 'Unique Key Column';  
GO  
```  
  
 Este exemplo retorna um conjunto de resultados chamado `Unique Key Column`, que exibe uma única linha contendo o nome da coluna de chave exclusiva da tabela Document, DocumentID. Observe que, se esta consulta continha um nome de índice inválido, se o nome de índice não correspondia à tabela, se a tabela não existia etc., será retornado NULL.  
  
##  <a name="disable"></a> Desabilitando ou Reabilitando uma tabela para indexação de texto completo  
 No [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], todos os bancos de dados criados pelo usuário são habilitados para texto completo por padrão. Além disso, uma tabela individual está automaticamente habilitada para indexação de texto completo desde que o índice de texto completo seja criado nela e uma coluna seja adicionada ao índice. Uma tabela está automaticamente desabilitada para indexação de texto completo quando a última coluna é descartada de seu índice de texto completo.  
  
 Em uma tabela que tenha um índice de texto completo, é possível desabilitar manualmente ou desabilitar de novo uma tabela para indexação de texto completo usando o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)].  
  
#### <a name="to-enable-a-table-for-full-text-indexing"></a>Para habilitar uma tabela para indexação de texto completo  
  
1.  Expanda o grupo do servidor, expanda **Bancos de Dados**e expanda o banco de dados que contém a tabela desejada para habilitação da indexação de texto completo.  
  
2.  Expanda **Tabelas**e clique com o botão direito do mouse na tabela que você quer desabilitar ou habilitar novamente para indexação de texto completo.  
  
3.  Selecione **Índice de Texto Completo**e clique em **Disable Full-Text index (Desabilitar Índice de Texto Completo)** ou **Enable Full-Text index (Habilitar Índice de Texto Completo)**.  
  
##  <a name="remove"></a> Removendo um índice de texto completo de uma tabela  
  
#### <a name="to-remove-a-full-text-index-from-a-table"></a>Para remover um índice de texto completo de uma tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela com o índice de texto completo a ser excluído.  
  
2.  Selecione **Excluir Índice de Texto Completo**.  
  
3.  Quando solicitado, clique em **OK** para confirmar que você deseja excluir o índice de texto completo.  
  
  
