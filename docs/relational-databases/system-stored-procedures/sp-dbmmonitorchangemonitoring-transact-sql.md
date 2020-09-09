---
description: sp_dbmmonitorchangemonitoring (Transact-SQL)
title: sp_dbmmonitorchangemonitoring (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_dbmmonitorchangemonitoring
- sp_dbmmonitorchangemonitoring_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sp_dbmmonitorchangemonitoring
- database mirroring [SQL Server], monitoring
ms.assetid: 17be755b-673d-4cd4-9544-6ecb4220bed3
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5ba2738f425a8240466cddca87a6d8cb6c5173bc
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89548183"
---
# <a name="sp_dbmmonitorchangemonitoring-transact-sql"></a>sp_dbmmonitorchangemonitoring (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Altera o valor de um parâmetro de monitoração de espelhamento de banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dbmmonitorchangemonitoring parameter  
    , value   
```  
  
## <a name="arguments"></a>Argumentos  
 *meter*  
 Especifica o identificador do parâmetro a ser alterado. Atualmente, apenas o seguinte parâmetro está disponível:  
  
 1 = Período de atualização  
  
 O número de minutos entre as atualizações da tabela de status do espelhamento de banco de dados. O intervalo padrão é de 1 minuto.  
  
 *value*  
 Especifica o novo valor do parâmetro que está sendo alterado.  
  
|Parâmetro|Descrição do valor|  
|---------------|--------------------------|  
|1|Um inteiro no intervalo de 1 a 120 que especifica um novo período de atualização, em minutos.|  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Nenhum  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  
  
## <a name="permissions"></a>Permissões  
 Exige associação à função de servidor fixa **sysadmin** .  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir altera o período de atualização para 5 minutos.  
  
```  
EXEC sp_dbmmonitorchangemonitoring 1, 5 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Monitorando o espelhamento de banco de dados &#40;SQL Server&#41;](../../database-engine/database-mirroring/monitoring-database-mirroring-sql-server.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitoraddmonitoring ](../../relational-databases/system-stored-procedures/sp-dbmmonitoraddmonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitordropmonitoring ](../../relational-databases/system-stored-procedures/sp-dbmmonitordropmonitoring-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_dbmmonitorhelpmonitoring ](../../relational-databases/system-stored-procedures/sp-dbmmonitorhelpmonitoring-transact-sql.md)   
 [sp_dbmmonitorresults &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-dbmmonitorresults-transact-sql.md)  
  
  
