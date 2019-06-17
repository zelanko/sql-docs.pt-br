---
title: sp_syscollector_set_cache_directory (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_directory_TSQL
- sp_syscollector_set_cache_directory
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_set_cache_directory stored procedure
ms.assetid: df56d5a5-8961-494f-a745-d752ca63805a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 300a59bb09fa28a626b117f51cfa6509b5ca883e
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63004281"
---
# <a name="spsyscollectorsetcachedirectory-transact-sql"></a>sp_syscollector_set_cache_directory (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Especifica o diretório em que os dados coletados são armazenados antes de serem carregados no data warehouse de gerenciamento.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_set_cache_directory [ @cache_directory = ] 'cache_directory'  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @cache_directory = ] 'cache_directory'` O diretório no sistema de arquivos onde os dados coletados são armazenados temporariamente. *cache_directory* está **nvarchar (255)** , com um valor padrão de NULL. Se nenhum valor for especificado, o valor temporário padrão do diretório do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será utilizado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Comentários  
 Você deve desabilitar o coletor de dados antes de alterar sua configuração do diretório de cache. Esse procedimento armazenado falhará se o coletor de dados estiver habilitado. Para obter mais informações, consulte [habilitar ou desabilitar a coleta de dados](../../relational-databases/data-collection/enable-or-disable-data-collection.md), e [gerenciar coleta de dados](../../relational-databases/data-collection/manage-data-collection.md).  
  
 O diretório especificado não precisa existir no momento em que o sp_syscollector_set_cache_directory for executado. Entretanto, os dados não serão armazenados em cache ou carregados com êxito até que o diretório seja criado. Recomenda-se criar o diretório antes de executar esse procedimento armazenado.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_admin (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desabilita o coletor de dados, define o diretório de cache para o coletor de dados `D:\tempdata`e, em seguida, habilita o coletor de dados.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXEC dbo.sp_syscollector_set_cache_directory N'D:\tempdata';  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de coletor de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/data-collector-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_window &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-window-transact-sql.md)  
  
  
