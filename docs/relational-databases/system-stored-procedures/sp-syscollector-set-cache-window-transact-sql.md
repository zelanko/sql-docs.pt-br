---
title: sp_syscollector_set_cache_window (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 08/09/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-stored-procedures
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_syscollector_set_cache_window
- sp_syscollector_set_cache_window_TSQL
dev_langs: TSQL
helpviewer_keywords:
- sp_syscollector_set_cache_window stored procedure
- data collector [SQL Server], stored procedures
ms.assetid: 660f2749-392f-46bf-89f3-27764d848507
caps.latest.revision: "23"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 9f9390255229779d2584fb0176c5651fa06cfb51
ms.sourcegitcommit: 2208a909ab09af3b79c62e04d3360d4d9ed970a7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/02/2018
---
# <a name="spsyscollectorsetcachewindow-transact-sql"></a>sp_syscollector_set_cache_window (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Define o número de vezes para tentativa de carregamento de dados no caso de falha. Tentar novamente um carregamento no caso de falha reduzirá o risco de perder os dados coletados.  

  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_syscollector_set_cache_window [ @cache_window = ] cache_window   
```  
  
## <a name="arguments"></a>Argumentos  
 [ @cache_window =] *cache_window*  
 É o número de vezes em que, depois de uma falha, há uma nova tentativa de carregamento de dados no data warehouse de gerenciamento sem perda dos dados. *cache_window* é **int** com um valor padrão de 1. *cache_window* pode ter um dos seguintes valores:  
  
|Valor|Description|  
|-----------|-----------------|  
|-1|Armazena em cache todos os dados de carregamento de falhas de carregamento anteriores.|  
|0|Não armazena em cache quaisquer dados de uma falha de carregamento.|  
|*n*|Armazenar em cache dados de n falhas de carregamento anteriores, onde  *n*  > = 1.|  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [sp_syscollector_set_cache_directory &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-syscollector-set-cache-directory-transact-sql.md)  
  
  
