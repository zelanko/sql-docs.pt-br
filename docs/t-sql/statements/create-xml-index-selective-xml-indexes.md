---
title: CREATE XML INDEX (índices XML seletivos) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: 1f510151-41d5-45c2-9cd0-b1ca0246fffe
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 3f5e9e831677a2779c908a0ec4b3afa5b27f7fff
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68058491"
---
# <a name="create-xml-index-selective-xml-indexes"></a>CREATE XML INDEX (índices XML seletivos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Cria um novo índice XML seletivo secundário em um único caminho que já foi indexado por um índice XML seletivo existente. Também é possível criar índices XML seletivos primários. Para obter informações, consulte [Criar, alterar e remover índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE XML INDEX index_name  
    ON <table_object> ( xml_column_name )  
    USING XML INDEX sxi_index_name  
    FOR ( <xquery_or_sql_values_path> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ database_name.schema_name.table_name | schema_name.table_name | table_name }  
  
<xquery_or_sql_values_path>::=   
<path_name>   
  
<path_name> ::=   
character string literal  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
xmlnamespace_uri AS xmlnamespace_prefix  
  
<index_options> ::=   
(    
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY = OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE = OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *index_name*  
 Nome do novo índice a ser criado. Os nomes de índice precisam ser exclusivos dentro de uma tabela, mas não precisam ser exclusivos dentro de um banco de dados. Os nomes de índice precisam seguir as regras para [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ON *\<table_object>* É a tabela que contém a coluna XML a ser indexada. Você também pode usar os seguintes formatos:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
 *xml_column_name*  
 Nome da coluna XML que contém o caminho a ser indexado.  
  
 USING XML INDEX *sxi_index_name*  
 Nome do índice XML seletivo existente.  
  
 FOR **(** \<xquery_or_sql_values_path> **)** É o nome do caminho indexado no qual o índice XML seletivo secundário será criado. O caminho a ser indexado é o nome atribuído da instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
 WITH \<index_options> Para obter informações sobre as opções de índice, consulte [CREATE XML INDEX](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>Comentários  
 Pode haver vários índices XML seletivos secundários em cada coluna XML na tabela base.  
  
## <a name="limitations-and-restrictions"></a>Limitações e Restrições  
 Deve existir um índice XML seletivo em uma coluna XML para que índices XML seletivos secundários possam ser criados na coluna.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um índice XML seletivo secundário no caminho `pathabc`. O caminho a ser indexado é o nome atribuído da instrução [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR ( pathabc );  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Criar, alterar e remover índices XML seletivos secundários](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)  
  
  

