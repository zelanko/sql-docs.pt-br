---
title: sp_syscollector_set_cache_window (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.prod_service: database-engine
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
caps.latest.revision: 23
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 3b5d457ff251535e483658f8be6bcdab847b5ee8
ms.sourcegitcommit: f1caaa156db2b16e817e0a3884394e7b30fb642f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2018
ms.locfileid: "33258757"
---
# <a name="spsyscollectorsetcachewindow-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define o número de vezes para tentativa de carregamento de dados no caso de falha. Tentar novamente um carregamento no caso de falha reduzirá o risco de perder os dados coletados.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cache_window = ] *cache_window*  
 É o número de vezes em que, depois de uma falha, há uma nova tentativa de carregamento de dados no data warehouse de gerenciamento sem perda dos dados. *cache_window* é **int** com um valor padrão de 1. *cache_window* pode ter um dos seguintes valores:  
  
|Value|Description|  
|-----------|-----------------|  
|-1|Armazena em cache todos os dados de carregamento de falhas de carregamento anteriores.|  
|0|Não armazena em cache quaisquer dados de uma falha de carregamento.|  
|*n*|Armazenar em cache dados de n falhas de carregamento anteriores, onde *n* > = 1.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 Você deve desabilitar o coletor de dados antes de alterar sua configuração de janela de cache. Esse procedimento armazenado falhará se o coletor de dados estiver habilitado. Para obter mais informações, consulte [habilitar ou desabilitar a coleta de dados](../../relational-databases/data-collection/enable-or-disable-data-collection.md), e [gerenciar coleta de dados](../../relational-databases/data-collection/manage-data-collection.md).  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados fixa dc_admin (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desabilita o coletor de dados, configura a janela de cache para reter os dados para até três carregamentos com falha e habilita o coletor de dados.  
  
```sql  
USE msdb;  
GO  
EXECUTE dbo.sp_syscollector_disable_collector;  
GO  
EXECUTE dbo.sp_syscollector_set_cache_window 3;  
GO  
EXECUTE dbo.sp_syscollector_enable_collector;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
