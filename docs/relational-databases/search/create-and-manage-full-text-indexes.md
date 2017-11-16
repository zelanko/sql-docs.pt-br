---
title: "Criar e gerenciar índices de texto completo | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: dbe-search
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: full-text indexes [SQL Server], about
ms.assetid: f8a98486-5438-44a8-b454-9e6ecbc74f83
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: On Demand
ms.openlocfilehash: 468a8c1d4b2b528b612684a93d571fca374db6cf
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="create-and-manage-full-text-indexes"></a>Criar e gerenciar índices de texto completo
Este tópico descreve como criar, popular e gerenciar índices de texto completo no SQL Server.
  
## <a name="prerequisite---create-a-full-text-catalog"></a>Pré-requisito – Criar um catálogo de texto completo
Antes de criar um índice de texto completo, é necessário ter um catálogo de texto completo. O catálogo é um contêiner virtual de um ou mais índices de texto completo. Para obter mais informações, consulte [Criar e gerenciar catálogos de texto completo](../../relational-databases/search/create-and-manage-full-text-catalogs.md).
  
##  <a name="tasks"></a> Criar, alterar ou remover um índice de texto completo  
### <a name="create-a-full-text-index"></a>Criar um índice de texto completo  
  
-   [CREATE FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-fulltext-index-transact-sql.md)  
  
### <a name="alter-a-full-text-index"></a>Alterar um índice de texto completo
  
-   [ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)  
  
### <a name="drop-a-full-text-index"></a>Remover um índice de texto completo 
  
-   [DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)

## <a name="populate-a-full-text-index"></a>Popular um índice de texto completo
O processo de criar e manter um índice de texto completo é chamado de *população* (também conhecido como *rastreamento*). Há três tipos de população de índice de texto completo:
-   População completa
-   População com base em controle de alterações
-   População incremental com base em um carimbo de data/hora.

Para obter mais informações, consulte [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).

##  <a name="view"></a> Exibir as propriedades de um índice de texto completo
### <a name="view-the-properties-of-a-full-text-index-with-transact-sql"></a>Exibir as propriedades de um índice de texto completo com o Transact-SQL
|Exibição de catálogo ou de gerenciamento dinâmico|Description|  
|----------------------------------------|-----------------|  
|[sys.fulltext_index_catalog_usages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-catalog-usages-transact-sql.md)|Retorna uma linha para cada catálogo de texto completo para referência de índice de texto completo.|  
|[sys.fulltext_index_columns &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-columns-transact-sql.md)|Contém uma linha para cada coluna que faz parte de um índice de texto completo.|  
|[sys.fulltext_index_fragments &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-index-fragments-transact-sql.md)|Um índice de texto completo usa tabelas internas, chamadas de fragmentos de índice de texto completo, para armazenar os dados de índices invertidos. Esta exibição pode ser usada para consultar os metadados sobre estes fragmentos. Esta exibição contém uma linha para cada fragmento de índice de texto completo em toda tabela que contém um índice de texto completo.|  
|[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)|Contém uma linha por índice de texto completo de um objeto tabular.|  
|[sys.dm_fts_index_keywords &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-transact-sql.md)|Retorna informações sobre o conteúdo de um índice de texto completo da tabela especificada.|  
|[sys.dm_fts_index_keywords_by_document &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-keywords-by-document-transact-sql.md)|Retorna informações sobre o conteúdo no nível de documento de um índice de texto completo da tabela especificada. Uma determinada palavra-chave pode aparecer em vários documentos.|  
|[sys.dm_fts_index_population &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-fts-index-population-transact-sql.md)|Retorna informações sobre as populações de índice de texto completo que estão em andamento.|  
 
### <a name="view-the-properties-of-a-full-text-index-with-management-studio"></a>Exibir as propriedades de um índice de texto completo com o Management Studio 
1.  No Management Studio, no Pesquisador de Objetos, expanda o servidor.  
  
2.  Expanda **Bancos de Dados**e expanda o banco de dados que contém o índice de texto completo.  
  
3.  Expanda **Tabelas**.  
  
4.  Clique com o botão direito do mouse na tabela em que o índice de texto completo está definido, selecione **Índice de Texto Completo**e, no menu de contexto **Índice de Texto Completo** , clique em **Propriedades**. Este procedimento abre a caixa de diálogo **Propriedades do Índice de Texto Completo** .  
  
5.  No painel **Selecionar uma página** , você pode selecionar qualquer uma das seguintes páginas:  
  
    |Página|Description|  
    |----------|-----------------|  
    |**Geral**|Exibe as propriedades básicas do índice de texto completo. Isso inclui várias propriedades modificáveis e uma série de propriedades inalteráveis, como o nome do banco de dados, o nome da tabela e o nome da coluna de chave de texto completo. As propriedades modificáveis são:<br /><br /> **Lista de palavras irrelevantes de índice de texto completo**<br /><br /> **Indexação de texto completo habilitada**<br /><br /> **Controle de alterações**<br /><br /> **Lista de propriedades de pesquisa**<br /><br />Para obter mais informações, consulte [Propriedades do Índice de Texto Completo &#40;página Geral&#41;](http://msdn.microsoft.com/library/f4dff61c-8c2f-4ff9-abe4-70a34421448f).|  
    |**Colunas**|Exibe as colunas da tabela que estão disponíveis para indexação de texto completo. A(s) coluna(s) selecionada(s) tem(têm) índice de texto completo. Você pode selecionar tantas colunas disponíveis quantas desejar para incluí-las no índice de texto completo. Para obter mais informações, consulte [Propriedades do Índice de Texto Completo &#40;página Colunas&#41;](http://msdn.microsoft.com/library/75e52edb-0d07-4393-9345-8b5af4561e35).|  
    |**Agendas**|Use esta página para criar ou gerenciar agendas para executar um trabalho do SQL Server Agent que inicia uma população incremental de tabela para as populações de índice de texto completo. Para obter mais informações, consulte [Popular índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).<br /><br /> Observação: depois que você sair da caixa de diálogo **Propriedades do Índice de Texto Completo** , qualquer agenda recém-criada será associada a um trabalho do SQL Server Agent (Iniciar População Incremental da Tabela em *database_name*.*table_name*).|  
  
6.  [!INCLUDE[clickOK](../../includes/clickok-md.md)] para salvar quaisquer alterações e sair da caixa de diálogo **Propriedades do índice de texto completo**.  
  
##  <a name="props"></a> Exibir as propriedades de colunas e tabelas indexadas  
 Muitas funções [!INCLUDE[tsql](../../includes/tsql-md.md)], como OBJECTPROPERTYEX, podem ser usadas para obter o valor de diversas propriedades de indexação de texto completo. Essas informações são úteis para administrar e solucionar problemas de pesquisa de texto completo.  
  
 A tabela a seguir lista as propriedades de texto completo relacionadas a colunas e tabelas indexadas e suas funções [!INCLUDE[tsql](../../includes/tsql-md.md)] relacionadas.  
  
|Propriedade|Descrição|Função|  
|--------------|-----------------|--------------|  
|**FullTextTypeColumn**|TYPE COLUMN na tabela que armazena as informações de tipo de documento da coluna.|[COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md)|  
|**IsFulltextIndexed**|Se uma coluna foi habilitada para indexação de texto completo.|COLUMNPROPERTY|  
|**IsFulltextKey**|Se o índice é a chave de texto completo de uma tabela.|[INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md)|  
|**TableFulltextBackgroundUpdateIndexOn**|Se uma tabela tem indexação de atualização de texto completo em segundo plano.|[OBJECTPROPERTYEX](../../t-sql/functions/objectpropertyex-transact-sql.md)|  
|**TableFulltextCatalogId**|ID do catálogo de texto completo no qual residem os dados de índice de texto completo da tabela.|OBJECTPROPERTYEX|  
|**TableFulltextChangeTrackingOn**|Se o controle de alterações de texto completo está habilitado em uma tabela.|OBJECTPROPERTYEX|  
|**TableFulltextDocsProcessed**|Número de linhas processadas desde o início da indexação de texto completo.|OBJECTPROPERTYEX|  
|**TableFulltextFailCount**|Número de linhas que a Pesquisa de Texto Completo não indexou.|OBJECTPROPERTYEX|  
|**TableFulltextItemCount**|Número de linhas que foram indexadas com texto completo com êxito.|OBJECTPROPERTYEX|  
|**TableFulltextKeyColumn**|A ID de coluna da coluna de chave exclusiva de texto completo.|OBJECTPROPERTYEX|  
|**TableFullTextMergeStatus**|Se uma tabela que tem um índice de texto completo está sendo mesclada.|OBJECTPROPERTYEX|  
|**TableFulltextPendingChanges**|Número de entradas de controle de alterações pendentes a serem processadas.|OBJECTPROPERTYEX|  
|**TableFulltextPopulateStatus**|Status de população de uma tabela de texto completo.|OBJECTPROPERTYEX|  
|**TableHasActiveFulltextIndex**|Se uma tabela tem um índice de texto completo ativo.|OBJECTPROPERTYEX|  
  
##  <a name="key"></a> Obtenha informações sobre a coluna de chave de texto completo  
 Normalmente, o resultado de funções com valor de conjunto de linhas CONTAINSTABLE ou FREETEXTTABLE precisam ser unidas à tabela base. Nesses casos, você precisa saber o nome da coluna de chave exclusiva. Você pode perguntar se um dado índice exclusivo é usado como chave de texto completo e pode obter o identificador da coluna de chave de texto completo.  
  
### <a name="determine-whether-a-given-unique-index-is-used-as-the-full-text-key-column"></a>Determinar se um dado índice exclusivo é usado como a coluna de chave de texto completo  
  
Use uma instrução [SELECT](../../t-sql/queries/select-transact-sql.md) para chamar a função [INDEXPROPERTY](../../t-sql/functions/indexproperty-transact-sql.md). Na chamada de função, use a função OBJECT_ID para converter o nome da tabela (*table_name*) na ID de tabela, especifique o nome de um índice exclusivo para a tabela e especifique a propriedade de índice **IsFulltextKey** da seguinte maneira:  
  
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
  
### <a name="find-the-identifier-of-the-full-text-key-column"></a>Localizar o identificador da coluna de chave de texto completo  
  
Cada tabela habilitada para texto completo tem uma coluna que é usada para impor linhas exclusivas da tabela (a *coluna de chave**exclusiva*). A propriedade **TableFulltextKeyColumn** , obtida da função OBJECTPROPERTYEX, contém a ID de coluna da coluna de chave exclusiva.  
 
Para obter esse identificador, você pode usar uma instrução SELECT para chamar a função OBJECTPROPERTYEX. Use a função OBJECT_ID para converter o nome da tabela (*table_name*) na ID de tabela e especifique a propriedade **TableFulltextKeyColumn** da seguinte maneira:  
  
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

## <a name="index-varbinarymax-and-xml-columns"></a>Indexar colunas varbinary(max) e xml  
 Se uma coluna **varbinary(max)**, **varbinary**ou **xml** tiver um índice de texto completo, ela poderá ser consultada usando os predicados (CONTAINS e FREETEXT) e as funções (CONTAINSTABLE e FREETEXTTABLE) de texto completo, como qualquer outra coluna indexada de texto completo.
   
### <a name="index-varbinarymax-or-varbinary-data"></a>Indexar dados varbinary(max) ou varbinary  
 Uma única coluna **varbinary (max)** ou **varbinary** pode armazenar vários tipos de documentos. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a qualquer tipo de documento para o qual um filtro está instalado e disponível no sistema operacional. O tipo de cada documento é identificado pela extensão de arquivo do documento. Por exemplo, no caso de uma extensão de arquivo .doc, a pesquisa de texto completo usa o filtro que dá suporte a documentos do Microsoft Word. Para obter uma lista dos tipos de documento disponíveis, veja a exibição de catálogo [sys.fulltext_document_types](../../relational-databases/system-catalog-views/sys-fulltext-document-types-transact-sql.md) .  
  
Observe que o Mecanismo de Texto Completo pode aproveitar os filtros existentes instalados no sistema operacional. Para que você possa usar filtros do sistema operacional, separadores de palavras e lematizadores, carregue-os na instância do servidor da seguinte maneira:  
  
```tsql  
EXEC sp_fulltext_service @action='load_os_resources', @value=1  
```  
  
Para criar um índice de texto completo em uma coluna **varbinary(max)** , o Mecanismo de Texto Completo precisa de acesso às extensões de arquivo dos documentos na coluna **varbinary(max)** . Esta informação deve ser armazenada em uma coluna de tabela, chamada de coluna de tipo, que deve estar associada à coluna **varbinary(max)** no índice de texto completo. Ao indexar um documento, o Mecanismo de Texto Completo utiliza a extensão de arquivo na coluna de tipo para identificar o filtro a ser usado.  
   
### <a name="index-xml-data"></a>Indexar dados xml  
 Uma coluna de tipo de dados **xml** armazena apenas fragmentos e documentos XML, e somente o filtro XML é usado para os documentos. Portanto, uma coluna de tipo é desnecessária. Em colunas **xml** , o índice de texto completo indexa o conteúdo dos elementos XML, mas ignora a marcação XML. Os valores de atributos são indexados como texto completo, a menos que sejam valores numéricos. Marcas de elemento são usadas como limites do token. Há suporte a fragmentos e documentos XML ou HTML bem formados que contêm vários idiomas.  
  
 Para obter mais informações sobre como indexar e fazer consultas em uma coluna **xml**, consulte [Usar a pesquisa de texto completo com colunas XML](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
##  <a name="disable"></a> Desabilitar ou reabilitar indexação de texto completo para uma tabela   
 No [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], todos os bancos de dados criados pelo usuário são habilitados para texto completo por padrão. Além disso, uma tabela individual está automaticamente habilitada para indexação de texto completo desde que o índice de texto completo seja criado nela e uma coluna seja adicionada ao índice. Uma tabela está automaticamente desabilitada para indexação de texto completo quando a última coluna é descartada de seu índice de texto completo.  
  
 Em uma tabela que tenha um índice de texto completo, é possível desabilitar manualmente ou desabilitar de novo uma tabela para indexação de texto completo usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  

1.  Expanda o grupo do servidor, expanda **Bancos de Dados**e expanda o banco de dados que contém a tabela desejada para habilitação da indexação de texto completo.  
  
2.  Expanda **Tabelas**e clique com o botão direito do mouse na tabela que você quer desabilitar ou habilitar novamente para indexação de texto completo.  
  
3.  Selecione **Índice de Texto Completo**e clique em **Disable Full-Text index (Desabilitar Índice de Texto Completo)** ou **Enable Full-Text index (Habilitar Índice de Texto Completo)**.  
  
##  <a name="remove"></a> Remover um índice de texto completo de uma tabela  
  
1.  No Pesquisador de Objetos, clique com o botão direito do mouse na tabela com o índice de texto completo a ser excluído.  
  
2.  Selecione **Excluir Índice de Texto Completo**.  
  
3.  Quando solicitado, clique em **OK** para confirmar que você deseja excluir o índice de texto completo.  
  
  
