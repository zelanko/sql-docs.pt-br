---
title: "Criar ÍNDICES XML (índices XML seletivos) | Microsoft Docs"
ms.custom: 
ms.date: 08/10/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs: TSQL
ms.assetid: 1f510151-41d5-45c2-9cd0-b1ca0246fffe
caps.latest.revision: "14"
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: b0cd1c2dd0c77409768e8ea7838724ca4d6b827e
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="create-xml-index-selective-xml-indexes"></a>CREATE XML INDEX (índices XML seletivos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Cria um novo índice XML seletivo secundário em um único caminho que já foi indexado por um índice XML seletivo existente. Também é possível criar índices XML seletivos primários. Para obter informações, consulte [Create, Alter e Drop os índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
CREATE XML INDEX index_name  
    ON <table_object> ( xml_column_name )  
    USING XML INDEX sxi_index_name  
    FOR ( <xquery_or_sql_values_path> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
  
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
 Nome do novo índice a ser criado. Os nomes de índice devem ser exclusivos dentro de uma tabela, mas não precisam ser exclusivos dentro de um banco de dados. Os nomes de índice devem seguir as regras de [identificadores](../../relational-databases/databases/database-identifiers.md).  
  
 ON  *\<table_object >* é a tabela que contém a coluna XML para indexação. Você também pode usar os seguintes formatos:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
 *xml_column_name*  
 Nome da coluna XML que contém o caminho a ser indexado.  
  
 USING XML INDEX *sxi_index_name*  
 Nome do índice XML seletivo existente.  
  
 PARA **(** \<xquery_or_sql_values_path > **)** é o nome do caminho indexado no qual criar o índice XML seletivo secundário. O caminho a ser indexado é o nome atribuído da instrução CREATE SELECTIVE XML INDEX. Para obter mais informações, veja [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
 COM \<index_options > para obter informações sobre as opções de índice, consulte [CREATE XML INDEX](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>Remarks  
 Pode haver vários índices XML seletivos secundários em cada coluna XML na tabela base.  
  
## <a name="limitations-and-restrictions"></a>Limitações e restrições  
 Deve existir um índice XML seletivo em uma coluna XML para que índices XML seletivos secundários possam ser criados na coluna.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Requer a permissão ALTER na tabela ou exibição. O usuário deve ser membro da função de servidor fixa **sysadmin** ou das funções de banco de dados fixas **db_ddladmin** e **db_owner** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir cria um índice XML seletivo secundário no caminho `pathabc`. O caminho para o índice é o nome atribuído a partir de [CREATE SELECTIVE XML INDEX &#40; Transact-SQL &#41; ](../../t-sql/statements/create-selective-xml-index-transact-sql.md).  
  
```  
CREATE XML INDEX filt_sxi_index_c  
ON Tbl(xmlcol)  
USING XML INDEX sxi_index  
FOR ( pathabc );  
```  
  
## <a name="see-also"></a>Consulte também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Criar, alterar e remover índices XML seletivos secundários](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md)  
  
  

