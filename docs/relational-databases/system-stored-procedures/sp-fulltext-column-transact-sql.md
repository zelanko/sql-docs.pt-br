---
title: sp_fulltext_column (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_fulltext_column_TSQL
- sp_fulltext_column
dev_langs:
- TSQL
helpviewer_keywords:
- sp_fulltext_column
ms.assetid: a84cc45d-1b50-44af-85df-2ea033b8a6a9
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e17a87a04c8c4286a66c6e7a0746f2d7de48d72
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68124336"
---
# <a name="spfulltextcolumn-transact-sql"></a>sp_fulltext_column (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-asdw-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-asdw-xxx-md.md)]

  Especifica se ou não uma determinada coluna de uma tabela participa da indexação de texto completo.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Use [ALTER FULLTEXT INDEX](../../t-sql/statements/alter-fulltext-index-transact-sql.md) em vez disso.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_fulltext_column [ @tabname= ] 'qualified_table_name' ,   
     [ @colname= ] 'column_name' ,   
     [ @action= ] 'action'   
     [ , [ @language= ] 'language_term' ]   
     [ , [ @type_colname= ] 'type_column_name' ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @tabname = ] 'qualified_table_name'` É um nome de tabela de uma ou duas partes. A tabela deve existir no banco de dados atual. A tabela deve ter um índice de texto completo. *qualified_table_name* está **nvarchar(517)** , sem nenhum valor padrão.  
  
`[ @colname = ] 'column_name'` É o nome de uma coluna na *qualified_table_name*. A coluna deve ser um caractere, **varbinary (max)** ou **imagem** coluna e não pode ser uma coluna computada. *column_name* está **sysname**, sem padrão.  
  
> [!NOTE]  
>  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode criar índices de texto completo de dados de texto armazenados em colunas que são de **varbinary (max)** ou **imagem** tipo de dados. Imagens e figuras não são indexadas.  
  
`[ @action = ] 'action'` É a ação a ser executada. *ação* está **varchar(20)** , sem nenhum valor padrão e pode ser um dos valores a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**add**|Adiciona *column_name* dos *qualified_table_name* para índice de texto completo inativo da tabela. Esta ação habilita a coluna para indexação de texto completo.|  
|**drop**|Remove *column_name* dos *qualified_table_name* do índice de texto completo inativo da tabela.|  
  
`[ @language = ] 'language_term'` É o idioma dos dados armazenados na coluna. Para obter uma lista dos idiomas incluídos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [sys. fulltext_languages &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-fulltext-languages-transact-sql.md).  
  
> [!NOTE]  
>  Use 'Neutro' quando uma coluna tiver dados em vários idiomas ou em um idioma sem-suporte. O padrão é especificado pela opção de configuração 'default full-text language.'  
  
`[ @type_colname = ] 'type_column_name'` É o nome de uma coluna na *qualified_table_name* que contém o tipo de documento da *column_name*. Essa coluna deve ser **char**, **nchar**, **varchar**, ou **nvarchar**. Ele é usado somente quando o tipo de dados *column_name* é do tipo **varbinary (max)** ou **imagem**. *type_column_name* está **sysname**, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="remarks"></a>Comentários  
 Se o índice de texto completo estiver ativo, qualquer população em andamento será interrompida. Além disso, se o controle de alterações estiver habilitado em uma tabela com um índice de texto completo ativo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] assegura que o índice seja atual. Por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] interrompe qualquer população atual na tabela, descarta o índice existente e inicia uma nova população.  
  
 Se o controle de alterações estiver ativo e for necessário adicionar ou descartar colunas do índice de texto completo, mas mantendo o índice preservado, a tabela deverá ser desativada e as colunas necessárias deverão ser adicionadas ou descartadas. Essas ações congelam o índice. A tabela pode ser ativada mais tarde, quando o início de uma população for praticável.  
  
## <a name="permissions"></a>Permissões  
 Usuário deve ser um membro do **db_ddladmin** fixo de função de banco de dados ou um membro do **db_owner** fixa a função de banco de dados ou o proprietário da tabela.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir adiciona a coluna `DocumentSummary` da tabela `Document` ao índice de texto completo da tabela.  
  
```  
USE AdventureWorks2012;  
GO  
EXEC sp_fulltext_column 'Production.Document', DocumentSummary, 'add';  
GO  
```  
  
 O exemplo a seguir supõe que você criou um índice de texto completo em uma tabela chamada `spanishTbl`. Para adicionar a coluna `spanishCol` ao índice de texto completo, execute o seguinte procedimento armazenado:  
  
```  
EXEC sp_fulltext_column 'spanishTbl', 'spanishCol', 'add', 0xC0A;  
GO  
```  
  
 Quando você executa esta consulta:  
  
```  
SELECT *   
FROM spanishTbl   
WHERE CONTAINS(spanishCol, 'formsof(inflectional, trabajar)')  
```  
  
 O conjunto de resultados inclui linhas com formas diferentes de `trabajar` (trabalhar), como `trabajo`, `trabajamos`e `trabajan`.  
  
> [!NOTE]  
>  Todas as colunas listadas em uma única cláusula de função de consulta de texto completo devem usar o mesmo idioma.  
  
## <a name="see-also"></a>Consulte também  
 [OBJECTPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/objectproperty-transact-sql.md)   
 [sp_help_fulltext_columns &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-transact-sql.md)   
 [sp_help_fulltext_columns_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-columns-cursor-transact-sql.md)   
 [sp_help_fulltext_tables &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-transact-sql.md)   
 [sp_help_fulltext_tables_cursor &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-tables-cursor-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Procedimentos armazenados de pesquisa de texto completo e pesquisa semântica &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/full-text-search-and-semantic-search-stored-procedures-transact-sql.md)  
  
  
