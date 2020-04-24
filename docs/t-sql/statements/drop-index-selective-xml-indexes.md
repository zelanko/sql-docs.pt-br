---
title: DROP INDEX (índices XML seletivos) | Microsoft Docs
ms.custom: ''
ms.date: 08/10/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- DROP XML INDEX statement
dev_langs:
- TSQL
ms.assetid: 4779ae84-e5f4-4d04-8fc1-e24a6631b428
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 912db4ce3841791e2bddde6f53be9869093bbcd2
ms.sourcegitcommit: 8ffc23126609b1cbe2f6820f9a823c5850205372
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/17/2020
ms.locfileid: "81636036"
---
# <a name="drop-index-selective-xml-indexes"></a>DROP INDEX (índices XML seletivos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Descarta um índice XML seletivo existente ou o índice XML seletivo secundário no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, consulte [Índices XML seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
DROP INDEX index_name ON <object>  
    [ WITH ( <drop_index_option> [ ,...n ] ) ]  
  
<object> ::=  
{ database_name.schema_name.table_or_view_name | schema_name.table_or_view_name | table_or_view_name }  
  
<drop_index_option> ::=  
{  
    MAXDOP = max_degree_of_parallelism  
    | ONLINE = { ON | OFF }  
}  
```  
  
##  <a name="arguments"></a><a name="Arguments"></a> Argumentos  
 *index_name*  
 Nome do índice existente a ser removido.  
  
 *\< object>* É a tabela que contém a coluna XML indexada. Use um destes formatos:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 *\<drop_index_option>* Para obter informações sobre as opções de descarte de índice, confira [DROP INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/drop-index-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 A permissão ALTER na tabela ou exibição é necessária para executar DROP INDEX. Essa permissão é concedida por padrão à função de servidor fixa sysadmin e às funções de banco de dados fixas db_ddladmin e db_owner.  
  
## <a name="example"></a>Exemplo  
 O exemplo a seguir mostra uma instrução DROP INDEX.  
  
```  
DROP INDEX sxi_index ON tbl;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Criar, alterar e remover índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)  
  
  

