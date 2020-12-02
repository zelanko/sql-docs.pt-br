---
description: CREATE FULLTEXT INDEX (Transact-SQL)
title: CREATE FULLTEXT INDEX (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 04/05/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- FULLTEXT_INDEX_TSQL
- CREATE_FULLTEXT_INDEX_TSQL
- CREATE FULLTEXT INDEX
- FULLTEXT INDEX
dev_langs:
- TSQL
helpviewer_keywords:
- full-text indexes [SQL Server], creating
- index creation [SQL Server], CREATE FULLTEXT INDEX statement
- CREATE FULLTEXT INDEX statement
ms.assetid: 8b80390f-5f8b-4e66-9bcc-cabd653c19fd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eac401156014952142c39851b1e703605997c245
ms.sourcegitcommit: 192f6a99e19e66f0f817fdb1977f564b2aaa133b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/25/2020
ms.locfileid: "96128006"
---
# <a name="create-fulltext-index-transact-sql"></a>CREATE FULLTEXT INDEX (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Cria um índice de texto completo em uma tabela ou em uma exibição indexada de um banco de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Somente um índice de texto completo é permitido por tabela ou exibição indexada, e cada índice de texto completo se aplica a uma única tabela ou exibição indexada. O índice de texto completo pode conter até 1024 colunas.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
CREATE FULLTEXT INDEX ON table_name  
   [ ( { column_name   
             [ TYPE COLUMN type_column_name ]  
             [ LANGUAGE language_term ]   
             [ STATISTICAL_SEMANTICS ]  
        } [ ,...n]   
      ) ]  
    KEY INDEX index_name   
    [ ON <catalog_filegroup_option> ]  
    [ WITH [ ( ] <with_option> [ ,...n] [ ) ] ]  
[;]  
  
<catalog_filegroup_option>::=  
 {  
    fulltext_catalog_name   
 | ( fulltext_catalog_name, FILEGROUP filegroup_name )  
 | ( FILEGROUP filegroup_name, fulltext_catalog_name )  
 | ( FILEGROUP filegroup_name )  
 }  
  
<with_option>::=  
 {  
   CHANGE_TRACKING [ = ] { MANUAL | AUTO | OFF [, NO POPULATION ] }   
 | STOPLIST [ = ] { OFF | SYSTEM | stoplist_name }  
 | SEARCH PROPERTY LIST [ = ] property_list_name   
 }  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
*table_name*       
É o nome da tabela ou exibição indexada que contém a coluna ou colunas incluídas no índice de texto completo.  
  
*column_name*       
É o nome da coluna incluída no índice de texto completo. Somente colunas do **char**, **varchar**, **nchar**, **nvarchar**, **text**, **ntext**, **image**, **xml** e **varbinary(max)** podem ser indexadas para pesquisa de texto completo. Para especificar várias colunas, repita a cláusula *column_name* da seguinte forma:  
  
CREATE FULLTEXT INDEX ON *table_name* (*column_name1* [...], *column_name2* [...]) ...  
  
TYPE COLUMN *type_column_name*       
Especifica o nome de uma coluna de tabela, *type_column_name*, usada para manter o tipo de um documento para um documento **varbinary(max)** ou **image** . Essa coluna, conhecida como coluna de tipo, contém uma extensão de arquivo fornecida pelo usuário (.doc, .pdf, .xls e assim por diante). A coluna de tipo deve ser do tipo **char**, **nchar**, **varchar**, ou **nvarchar**.  
  
Especifique TYPE COLUMN *type_column_name* somente se *column_name* especificar uma coluna **varbinary(max)** ou **image** na qual os dados são armazenados como dados binários. Caso contrário, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
> [!NOTE]  
> No momento da indexação, o Mecanismo de Texto Completo usa a abreviação na coluna de tipo de cada linha da tabela para identificar o filtro de pesquisa de texto completo que deve ser usado para o documento no *column_name*. O filtro carrega o documento como um fluxo binário, remove as informações de formatação e envia o texto do documento para o componente do separador de palavras. Para obter mais informações, veja [Configurar e gerenciar filtros para pesquisa](../../relational-databases/search/configure-and-manage-filters-for-search.md).  
  
LANGUAGE *language_term*       
É o idioma dos dados armazenados em *column_name*.  
  
*language_term* é opcional e pode ser especificado como uma cadeia de caracteres, um inteiro ou um valor hexadecimal que corresponda ao LCID (identificador de localidade) de um idioma. Se nenhum valor for especificado, o idioma padrão da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será usado.  
  
Se *language_term* for especificado, o idioma que ele representa será usado para indexar dados armazenados nas colunas **char**, **nchar**, **varchar**, **nvarchar**, **text** e **ntext**. Esse será o idioma padrão usado na hora da consulta se *language_term* não estiver especificado como parte de um predicado de texto completo em relação à coluna.  
  
Quando especificado como uma cadeia de caracteres, *language_term* corresponde ao valor da coluna alias na tabela do sistema syslanguages. A cadeia de caracteres precisa ser colocada entre aspas, como em **'** _language\_term_ **'** . Quando especificado como um inteiro, *language_term* é a LCID real que identifica o idioma. Quando especificado como um valor hexadecimal, *language_term* é 0x seguido pelo valor hexadecimal da LCID. O valor hexadecimal não deve exceder oito dígitos, incluindo zeros à esquerda.  
  
Se o valor estiver no formato DBCS (conjunto de caracteres de dois bytes), o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o converterá em Unicode.  
  
Os recursos, como separadores e lematizadores de palavras, devem estar habilitados para o idioma especificado como *language_term*. Se tais recursos não aceitarem o idioma especificado, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
Use o procedimento armazenado sp_configure para acessar informações sobre o idioma de texto completo da instância [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [sp_configure &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md).  
  
Para colunas não BLOB e não XML que contêm dados de texto em vários idiomas ou casos em que o idioma do texto armazenado na coluna é desconhecido, talvez seja necessário usar o recurso de idioma neutro (0x0). Porém, primeiro você deve compreender as possíveis consequências de usar o recurso de idioma neutro (0x0). Para obter informações sobre as possíveis soluções e consequências de usar o recurso neutro de idioma (0x0), veja [Escolher um idioma ao criar um índice de texto completo](../../relational-databases/search/choose-a-language-when-creating-a-full-text-index.md).  
  
Para documentos armazenados em colunas do tipo XML ou BLOB, a codificação de idioma do documento será usada no momento da indexação. Por exemplo, em colunas XML, o atributo **xml:lang** em documentos XML identificará o idioma. No momento da consulta, o valor especificado anteriormente em *language_term* se torna o idioma padrão usado para consultas de texto completo, a menos que *language_term* seja especificado como parte de uma consulta de texto completo.  
  
STATISTICAL_SEMANTICS       
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior) 
  
Cria a frase-chave adicional e índices de similaridade de documentos que fazem parte da indexação semântica estatística. Para obter mais informações, veja [Pesquisa semântica &#40;SQL Server&#41;](../../relational-databases/search/semantic-search-sql-server.md).  
  
KEY INDEX *index_name*       
É o nome do índice de chave exclusiva no *table_name*. O KEY INDEX deve ser uma coluna exclusiva de chave única, não anulável. Selecione o menor índice de chave exclusiva para a chave exclusiva de texto completo.  Para obter o melhor desempenho, recomendamos um tipo de dados de inteiro para a chave de texto completo.  
  
*fulltext_catalog_name*       
É o catálogo de texto completo usado para o índice de texto completo. O catálogo já deve existir no banco de dados. Esta cláusula é opcional. Se não estiver especificado, um catálogo padrão será usado. Se não existir nenhum catálogo padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] retornará um erro.  
  
FILEGROUP *filegroup_name*       
Cria o índice de texto completo especificado no grupo de arquivos especificado. O grupo de arquivos já deve existir. Se a cláusula FILEGROUP não for especificada, o índice de texto completo será colocado no mesmo grupo de arquivos que a tabela base, na exibição de uma tabela não particionada ou em um grupo de arquivos primário de uma tabela particionada.  
  
 CHANGE_TRACKING [ = ] { MANUAL | **AUTO** | OFF [ , NO POPULATION ] }       
 Especifica se as alterações (atualizações, exclusões ou inserções) feitas nas colunas da tabela que estão cobertas pelo índice de texto completo serão propagadas pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para o índice de texto completo. As alterações de dados por meio de WRITETEXT e UPDATETEXT não são refletidas no índice de texto completo e não são coletadas com o controle de alterações.  
  
MANUAL       
Especifica que as alterações controladas devem ser propagadas manualmente chamando-se a instrução ALTER FULLTEXT INDEX ... Instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] START UPDATE POPULATION (*preenchimento manual*). É possível usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent para chamar essa instrução [!INCLUDE[tsql](../../includes/tsql-md.md)] periodicamente.  
  
**AUTO**       
Especifica que as alterações controladas serão propagadas automaticamente conforme os dados forem modificados na tabela base (*preenchimento automático*). Embora sejam propagadas automaticamente, talvez essas alterações não se reflitam imediatamente no índice de texto completo. AUTO é o padrão.  
  
OFF [ `,` NO POPULATION]       
Especifica que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não mantém uma lista de alterações nos dados indexados. Quando a opção NO POPULATION não está especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] popula o índice completamente depois que ele é criado.  
  
A opção NO POPULATION pode ser usada apenas quando CHANGE_TRACKING está OFF. Quando a opção NO POPULATION está especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não popula um índice depois que ele é criado. O índice somente será preenchido depois que o usuário executar o comando ALTER FULLTEXT INDEX com a cláusula START FULL POPULATION ou START INCREMENTAL POPULATION.  
  
STOPLIST [ = ] { OFF | **SYSTEM** | *stoplist_name* }       
Associa uma lista de palavras irrelevantes de texto completo ao índice. O índice não é populado com nenhum token que faça parte da lista de palavras irrelevantes especificada. Se STOPLIST não estiver especificada, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associará a lista de palavras irrelevantes de texto completo ao índice.  
  
OFF       
Especifica que nenhuma lista de palavras irrelevantes seja associada ao índice de texto completo.  
  
**SYSTEM**       
Especifica que a lista de palavras irrelevantes do sistema de texto completo padrão deve ser usada para esse índice de texto completo.  
  
*stoplist_name*       
Especifica o nome da lista de palavras irrelevantes que deve ser associada ao índice de texto completo.  
  
SEARCH PROPERTY LIST [ = ] *property_list_name*       
**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] e posterior)  
  
Associa uma lista de propriedades de pesquisa ao índice.  
 
OFF       
Especifica que nenhuma lista de propriedades será associada ao índice de texto completo.  
  
*property_list_name*       
Especifica o nome da lista de propriedades de pesquisa para associar ao índice de texto completo.  
  
## <a name="remarks"></a>Comentários  
Para obter mais informações sobre índices de texto completo, veja [Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md).  
  
Em colunas **xml**, você pode criar um índice de texto completo que indexa o conteúdo dos elementos XML, mas ignora a marcação XML. Os valores de atributos são indexados como texto completo, a menos que sejam valores numéricos. Marcas de elemento são usadas como limites do token. Há suporte a fragmentos e documentos XML ou HTML bem formados que contêm vários idiomas. Para obter mais informações, veja [Usar a pesquisa de texto completo com colunas XML](../../relational-databases/xml/use-full-text-search-with-xml-columns.md).  
  
Recomendamos que a coluna de chave de índice seja de um tipo de dados inteiro. Isso otimiza o tempo de execução da consulta.  
  
## <a name="interactions-of-change-tracking-and-no-population-parameter"></a>Interações do controle de alterações e do parâmetro NO POPULATION  
 O fato de o índice de texto completo ser populado depende de o controle de alterações estar habilitado e de WITH NO POPULATION ter sido especificado na instrução ALTER FULLTEXT INDEX. A tabela a seguir resume o resultado da interação.  
  
|Controle de Alterações|WITH NO POPULATION|Result|  
|---------------------|------------------------|------------|  
|Não habilitado|Não especificado|Uma população completa é executada no índice.|  
|Não habilitado|Especificado|Não ocorre nenhuma população do índice até que uma instrução ALTER FULLTEXT INDEX...START POPULATION seja emitida.|  
|habilitado|Especificado|É gerado um erro e o índice não é alterado.|  
|habilitado|Não especificado|Uma população completa é executada no índice.|  
  
 Para obter mais informações sobre o preenchimento de índices de texto completo, veja [Preencher índices de texto completo](../../relational-databases/search/populate-full-text-indexes.md).  
  
## <a name="permissions"></a>Permissões  
 O usuário deve ter a permissão `REFERENCES` no catálogo de texto completo e a permissão `ALTER` na tabela ou exibição indexada, ou ser membro da função de servidor fixa `sysadmin` ou das funções de banco de dados fixas `db_owner` ou `db_ddladmin`.  
  
Se a opção `SET STOPLIST` estiver especificada, o usuário deve ter permissão REFERENCES na lista de palavras irrelevantes especificada. O proprietário da STOPLIST pode conceder essa permissão.  
  
> [!NOTE]  
> O público recebe a permissão REFERENCE para a lista de palavras irrelevantes (stoplist) padrão fornecida com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-creating-a-unique-index-a-full-text-catalog-and-a-full-text-index"></a>a. Criando um índice exclusivo, um catálogo de texto completo e um índice de texto completo  
 O exemplo a seguir cria um índice exclusivo na coluna `JobCandidateID` da tabela `HumanResources.JobCandidate` do banco de dados de exemplo [!INCLUDE[ssSampleDBnormal](../../includes/sssampledbnormal-md.md)]. Em seguida, o exemplo cria um catálogo de texto completo padrão, `ft`. Finalmente, o exemplo cria um índice de texto completo na coluna `Resume`, usando o catálogo `ft` e a lista de palavras irrelevantes (stoplist) do sistema.  
  
```sql  
CREATE UNIQUE INDEX ui_ukJobCand ON HumanResources.JobCandidate(JobCandidateID);  
CREATE FULLTEXT CATALOG ft AS DEFAULT;  
CREATE FULLTEXT INDEX ON HumanResources.JobCandidate(Resume)   
   KEY INDEX ui_ukJobCand   
   WITH STOPLIST = SYSTEM;  
GO  
```  
  
### <a name="b-creating-a-full-text-index-on-several-table-columns"></a>B. Criando um índice de texto completo em várias colunas da tabela  
 O exemplo a seguir cria um catálogo de texto completo, `production_catalog`, no banco de dados de exemplo `AdventureWorks`. Em seguida, o exemplo cria um índice de texto completo que usa esse novo catálogo. O índice de texto completo está nas colunas `ReviewerName`, `EmailAddress` e `Comments` de `Production.ProductReview`. Para cada coluna, o exemplo especifica o LCID de inglês, `1033` que é o idioma dos dados nas colunas. Esse índice de texto completo usa um índice de chave exclusiva existente, `PK_ProductReview_ProductReviewID`. Conforme recomendado, essa chave de índice está em uma coluna de inteiros, `ProductReviewID`.  
  
```sql  
CREATE FULLTEXT CATALOG production_catalog;  
GO  
CREATE FULLTEXT INDEX ON Production.ProductReview  
 (   
  ReviewerName  
     Language 1033,  
  EmailAddress  
     Language 1033,  
  Comments   
     Language 1033       
 )   
  KEY INDEX PK_ProductReview_ProductReviewID   
      ON production_catalog;   
GO  
```  
  
### <a name="c-creating-a-full-text-index-with-a-search-property-list-without-populating-it"></a>C. Criando um índice de texto completo com uma lista de propriedades de pesquisa sem populá-lo  
 O índice de texto completo está nas colunas `Title`, `DocumentSummary` e `Document` da tabela `Production.Document`. O exemplo especifica o LCID de inglês, `1033`, que é o idioma dos dados nas colunas. Esse índice de texto completo usa o catálogo de texto completo padrão e um índice de chave exclusiva existente, `PK_Document_DocumentID`. Conforme recomendado, essa chave de índice está em uma coluna de inteiros, `DocumentID`.  
  
 O exemplo especifica a lista de palavras irrelevantes do sistema. Também especifica uma lista de propriedades de pesquisa, `DocumentPropertyList`; para obter um exemplo que crie esta lista de propriedades, veja [CREATE SEARCH PROPERTY LIST &#40;Transact-SQL&#41;](../../t-sql/statements/create-search-property-list-transact-sql.md).  
  
 O exemplo especifica que o controle de alterações está desativado sem nenhuma população. Posteriormente, fora do horário de pico, o exemplo usa uma instrução ALTER FULLTEXT INDEX para iniciar uma população completa no novo índice e habilitar o controle de alterações automático.  
  
```sql  
CREATE FULLTEXT INDEX ON Production.Document  
  (   
  Title  
      Language 1033,   
  DocumentSummary  
      Language 1033,   
  Document   
      TYPE COLUMN FileExtension  
      Language 1033   
  )  
  KEY INDEX PK_Document_DocumentID  
          WITH STOPLIST = SYSTEM, SEARCH PROPERTY LIST = DocumentPropertyList, CHANGE_TRACKING OFF, NO POPULATION;  
   GO  
```  
  
 Posteriormente, fora do horário de pico, o índice é populado:  
  
```sql  
ALTER FULLTEXT INDEX ON Production.Document SET CHANGE_TRACKING AUTO;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
[Criar e gerenciar índices de texto completo](../../relational-databases/search/create-and-manage-full-text-indexes.md)       
[ALTER FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/alter-fulltext-index-transact-sql.md)       
[DROP FULLTEXT INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-fulltext-index-transact-sql.md)       
[Pesquisa de Texto Completo](../../relational-databases/search/full-text-search.md)       
[GRANT &#40;Transact-SQL&#41;](../../t-sql/statements/grant-transact-sql.md)       
[sys.fulltext_indexes &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-indexes-transact-sql.md)       
[Pesquisar propriedades de documento com listas de propriedades de pesquisa](../../relational-databases/search/search-document-properties-with-search-property-lists.md)       
  
  
