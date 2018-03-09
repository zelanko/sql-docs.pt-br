---
title: "Instrução ALTER INDEX (índices XML seletivos) | Microsoft Docs"
ms.custom: 
ms.date: 05/01/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|statements
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
dev_langs:
- TSQL
ms.assetid: cca96a8f-7737-42d2-bbcc-03d5f858dcc1
caps.latest.revision: 
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 9f875f7d34c568bc1156c5f8bce60d893fce8039
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="alter-index-selective-xml-indexes"></a>ALTER INDEX (índices XML seletivos)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Modifica um índice XML seletivo existente. A instrução ALTER INDEX altera um ou mais dos seguintes itens:  
  
-   A lista de caminhos indexados (cláusula FOR).  
  
-   A lista de namespaces (cláusula WITH XMLNAMESPACES).  
  
-   As opções de índice (cláusula WITH).  
  
 Você não pode alterar índices XML seletivos secundários. Para obter mais informações, consulte [Create, Alter e Drop índices XML seletivos secundários](../../relational-databases/xml/create-alter-and-drop-secondary-selective-xml-indexes.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
ALTER INDEX index_name  
    ON <table_object>   
    [WITH XMLNAMESPACES ( <xmlnamespace_list> )]  
    FOR ( <promoted_node_path_action_list> )  
    [WITH ( <index_options> )]  
  
<table_object> ::=   
{ [database_name. [schema_name ] . | schema_name. ] table_name }  
<promoted_node_path_action_list> ::=   
<promoted_node_path_action_item> [, <promoted_node_path_action_list>]  
  
<promoted_node_path_action_item>::=   
<add_node_path_item_action> | <remove_node_path_item_action>  
  
<add_node_path_item_action> ::=  
ADD <path_name> = <promoted_node_path_item>  
  
<promoted_node_path_item>::=  
<xquery_node_path_item> | <sql_values_node_path_item>  
  
<remove_node_path_item_action> ::= REMOVE <path_name>   
  
<path_name_or_typed_node_path>::=   
<path_name> | <typed_node_path>  
  
<typed_node_path> ::=   
<node_path> [[AS XQUERY <xsd_type_ext>] | [AS SQL <sql_type>]]  
  
<xquery_node_path_item> ::=   
<node_path> [AS XQUERY <xsd_type_or_node_hint>] [SINGLETON]  
  
<xsd_type_or_node_hint> ::=   
[<xsd_type>] [MAXLENGTH(x)] | 'node()'  
  
<sql_values_node_path_item> ::=   
<node_path> AS SQL <sql_type> [SINGLETON]  
  
<node_path> ::=   
character_string_literal  
  
<xsd_type_ext> ::=   
character_string_literal  
  
<sql_type> ::=   
identifier  
  
<path_name> ::=   
identifier  
  
<xmlnamespace_list> ::=   
<xmlnamespace_item> [, <xmlnamespace_list>]  
  
<xmlnamespace_item> ::=   
<xmlnamespace_uri> AS <xmlnamespace_prefix>  
  
<xml_namespace_uri> ::= character_string_literal  
<xml_namespace_prefix> ::= identifier  
  
<index_options> ::=   
(   
  | PAD_INDEX  = { ON | OFF }  
  | FILLFACTOR = fillfactor  
  | SORT_IN_TEMPDB = { ON | OFF }  
  | IGNORE_DUP_KEY =OFF  
  | DROP_EXISTING = { ON | OFF }  
  | ONLINE =OFF  
  | ALLOW_ROW_LOCKS = { ON | OFF }  
  | ALLOW_PAGE_LOCKS = { ON | OFF }  
  | MAXDOP = max_degree_of_parallelism  
)  
```  
  
##  <a name="Arguments"></a> Argumentos  
 *index_name*  
 Nome do índice existente a ser alterado.  
  
 *\<table_object >*  
 Tabela que contém a coluna XML a ser indexada. Use um destes formatos:  
  
-   `database_name.schema_name.table_name`  
  
-   `database_name..table_name`  
  
-   `schema_name.table_name`  
  
-   `table_name`  
  
 [WITH XMLNAMESPACES **(** \<xmlnamespace_list > **)**]  
 Lista de namespaces usados pelos caminhos a serem indexados. Para obter informações sobre a sintaxe da cláusula WITH XMLNAMESPACES, consulte [WITH XMLNAMESPACES &#40; Transact-SQL &#41; ](../../t-sql/xml/with-xmlnamespaces.md).  
  
 PARA **(** \<promoted_node_path_action_list > **)**  
 Lista de caminhos indexados a serem adicionados ou removidos.  
  
-   **Adicione um caminho.** Ao usar ADD para adicionar um caminho, use a mesma sintaxe usada para criar caminhos com a instrução CREATE SELECTIVE XML INDEX. Para obter informações sobre os caminhos que você pode especificar na instrução CREATE ou ALTER, consulte [especificar caminhos e dicas de otimização para índices XML seletivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md).  
  
-   **Remova um caminho.** Ao usar REMOVE para remover um caminho, forneça o nome que foi atribuído ao caminho quando ele foi criado.  
  
 [Com **(** \<index_options > **)**]  
 Você só pode especificar \<index_options > quando você usar ALTER INDEX sem a cláusula FOR. Quando você usar ALTER INDEX para adicionar ou remover caminhos no índice, as opções de índice não serão argumentos válidos. Para obter informações sobre as opções de índice, consulte [CREATE XML INDEX &#40; Índices XML seletivos &#41; ](../../t-sql/statements/create-xml-index-selective-xml-indexes.md).  
  
## <a name="remarks"></a>Remarks  
  
> [!IMPORTANT]  
>  Quando você executa uma instrução ALTER INDEX, o índice XML seletivo é sempre recriado. Considere o impacto desse processo em recursos do servidor.  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Para executar ALTER INDEX, a permissão ALTER na tabela ou exibição é necessária.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir mostra uma instrução ALTER INDEX. Essa instrução adiciona o caminho `'/a/b/m'` à parte XQuery do índice e exclui o caminho `'/a/b/e'` da parte SQL do índice criado no exemplo no tópico [CREATE SELECTIVE XML INDEX &#40;Transact-SQL&#41;](../../t-sql/statements/create-selective-xml-index-transact-sql.md). O caminho a ser excluído é identificado pelo nome atribuído a ele quando foi criado.  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
FOR   
(  
    ADD pathm = '/a/b/m' as XQUERY 'node()' ,  
    REMOVE pathabe  
);  
```  
  
 O exemplo a seguir mostra uma instrução ALTER INDEX que especifica opções de índice. As opções de índice são permitidas porque a instrução não usa uma cláusula FOR para adicionar ou remover caminhos.  
  
```sql  
ALTER INDEX sxi_index  
ON Tbl  
PAD_INDEX = ON;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Índices XML Seletivos &#40;SXI&#41;](../../relational-databases/xml/selective-xml-indexes-sxi.md)   
 [Criar, alterar e remover índices XML seletivos](../../relational-databases/xml/create-alter-and-drop-selective-xml-indexes.md)   
 [Especificar caminhos e dicas de otimização para índices XML seletivos](../../relational-databases/xml/specify-paths-and-optimization-hints-for-selective-xml-indexes.md)  
  
  
