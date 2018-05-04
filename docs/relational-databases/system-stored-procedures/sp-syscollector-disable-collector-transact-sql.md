---
title: sp_syscollector_disable_collector (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_syscollector_disable_collector_TSQL
- sp_syscollector_disable_collector
dev_langs:
- TSQL
helpviewer_keywords:
- data collector [SQL Server], stored procedures
- sp_syscollector_disable_collector
ms.assetid: 9ef4c85d-cca6-452d-94be-2be6f616c3d8
caps.latest.revision: 17
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 8b80416f0c635dfa9e9f4be63547cbbb40e5b6e6
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spsyscollectordisablecollector-transact-sql"></a>sp_syscollector_disable_collector (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Desabilita o coletor de dados. Como há apenas um coletor de dados por servidor, nenhum parâmetro é necessário.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dbo.sp_syscollector_disable_collector   
```  
  
## <a name="arguments"></a>Argumentos  
 Nenhuma  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 **0** (êxito) ou **1** (falha)  
  
## <a name="remarks"></a>Remarks  
 Assume o coletor de dados no servidor como padrão.  
  
## <a name="permissions"></a>Permissões  
 É necessária a associação na função de banco de dados fixa **dc_admin** ou **dc_operator** (com a permissão EXECUTE) para executar esse procedimento.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir desabilita o coletor de dados.  
  
```  
EXEC dbo.sp_syscollector_disable_collector;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/system-stored-procedures-transact-sql.md)   
 [Coleta de Dados](../../relational-databases/data-collection/data-collection.md)  
  
  
