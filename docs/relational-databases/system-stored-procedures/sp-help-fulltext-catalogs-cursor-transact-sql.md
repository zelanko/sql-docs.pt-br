---
title: sp_help_fulltext_catalogs_cursor (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_help_fulltext_catalogs_cursor
- sp_help_fulltext_catalogs_cursor_TSQL
dev_langs: TSQL
helpviewer_keywords: sp_help_fulltext_catalogs_cursor
ms.assetid: d44478d1-0cc4-415e-9d1a-6dccb64674fa
caps.latest.revision: "33"
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a1d6bafa75fc4962ee9b7c263f8fc08204da67fd
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="sphelpfulltextcatalogscursor-transact-sql"></a>sp_help_fulltext_catalogs_cursor (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-asdb-xxxx-xxx-md.md)]

  Usa um cursor para retornar a ID, o nome, o diretório raiz, o status e o número de tabelas indexadas de texto completo para o catálogo de texto completo especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]Use o [fulltext_catalogs](../../relational-databases/system-catalog-views/sys-fulltext-catalogs-transact-sql.md) exibição do catálogo.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] até a [versão atual](http://go.microsoft.com/fwlink/p/?LinkId=299658)), [!INCLUDE[sqldbesa](../../includes/sqldbesa-md.md)].|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_help_fulltext_catalogs_cursor [ @cursor_return= ] @cursor_variable OUTPUT ,   
     [ @fulltext_catalog_name = ] 'fulltext_catalog_name'   
```  
  
## <a name="arguments"></a>Argumentos  
 [  **@cursor_return=**]  *@cursor_variable*  **SAÍDA**  
 É a variável de saída do tipo **cursor**. O cursor é somente leitura, rolável e dinâmico.  
  
 [  **@fulltext_catalog_name=**] **'***fulltext_catalog_name***'**  
 É o nome do catálogo de texto completo. *fulltext_catalog_name* é **sysname**. Se este parâmetro for omitido ou for NULL, serão retornadas informações sobre todos os catálogos de texto completo associados ao banco de dados atual.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou (1) falha  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|**fulltext_catalog_id**|**smallint**|Identificador do catálogo de texto completo.|  
|**NOME**|**sysname**|Nome do catálogo de texto completo.|  
|**CAMINHO**|**nvarchar (260)**|A partir do [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], esta cláusula não tem nenhum efeito.|  
|**STATUS**|**int**|Status de população do índice de texto completo do catálogo:<br /><br /> 0 = Ocioso<br /><br /> 1 = População completa em andamento<br /><br /> 2 = Pausado<br /><br /> 3 = Acelerado<br /><br /> 4 = Recuperando<br /><br /> 5 = Desligado<br /><br /> 6 = População incremental em andamento<br /><br /> 7 = Construindo índice<br /><br /> 8 = O disco está cheio. Em Pausa<br /><br /> 9 = Controle de alterações|  
|**NUMBER_FULLTEXT_TABLES**|**int**|Número de tabelas de texto completo indexadas associadas ao catálogo.|  
  
## <a name="permissions"></a>Permissões  
 As permissões de execução têm como padrão a função **public** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir retorna informações sobre o catálogo de texto completo `Cat_Desc`.  
  
```  
USE AdventureWorks2012;  
GO  
DECLARE @mycursor CURSOR;  
EXEC sp_help_fulltext_catalogs_cursor @mycursor OUTPUT, 'Cat_Desc';  
FETCH NEXT FROM @mycursor;  
WHILE (@@FETCH_STATUS <> -1)  
   BEGIN  
      FETCH NEXT FROM @mycursor;  
   END  
CLOSE @mycursor;  
DEALLOCATE @mycursor;  
GO   
```  
  
## <a name="see-also"></a>Consulte também  
 [FULLTEXTCATALOGPROPERTY &#40; Transact-SQL &#41;](../../t-sql/functions/fulltextcatalogproperty-transact-sql.md)   
 [sp_fulltext_catalog &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-fulltext-catalog-transact-sql.md)   
 [sp_help_fulltext_catalogs &#40; Transact-SQL &#41;](../../relational-databases/system-stored-procedures/sp-help-fulltext-catalogs-transact-sql.md)   
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)  
  
  
