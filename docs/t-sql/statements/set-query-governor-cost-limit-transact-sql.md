---
title: SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT
- SET_QUERY_GOVERNOR_COST_LIMIT_TSQL
- QUERY_GOVERNOR_COST_LIMIT
- QUERY_GOVERNOR_COST_LIMIT_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- SET QUERY_GOVERNOR_COST_LIMIT statement
- connections [SQL Server], overriding
- QUERY_GOVERNOR_COST_LIMIT option
- overriding connection values
ms.assetid: 3424bb44-6915-462d-a8d7-fe834af81387
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 20eaa69a9c0f07926d937128a7fc10c43d4128ef
ms.sourcegitcommit: edba1c570d4d8832502135bef093aac07e156c95
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/20/2020
ms.locfileid: "86484327"
---
# <a name="set-query_governor_cost_limit-transact-sql"></a>SET QUERY_GOVERNOR_COST_LIMIT (Transact-SQL)
[!INCLUDE [SQL Server SQL Database](../../includes/applies-to-version/sql-asdb.md)]

  Substitui o valor **query governor cost limit** atualmente configurado da conexão atual.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql
  
SET QUERY_GOVERNOR_COST_LIMIT value  
```  
  
[!INCLUDE[sql-server-tsql-previous-offline-documentation](../../includes/sql-server-tsql-previous-offline-documentation.md)]

## <a name="arguments"></a>Argumentos
 *value*  
 É um valor numérico ou inteiro que especifica o tempo mais longo de execução de uma consulta. Os valores são arredondados para baixo, para o inteiro mais próximo. Os valores negativos são arredondados para 0. O administrador de consultas não permite a execução de qualquer consulta que tem um custo calculado que excede aquele valor. Se for especificado 0 (o padrão) para essa opção, o administrador de consultas será desativado e todas as consultas terão permissão para serem executadas indefinidamente.  
  
 "Custo da consulta" faz referência a um tempo decorrido estimado em segundos, exigido para concluir uma consulta em uma configuração de hardware específica.  
  
## <a name="remarks"></a>Comentários  
 O uso de SET QUERY_GOVERNOR_COST_LIMIT se aplica somente à conexão atual e persiste durante a conexão atual. Use a opção [Configurar a opção query governor cost limit de configuração do servidor](../../database-engine/configure-windows/configure-the-query-governor-cost-limit-server-configuration-option.md) de **sp_configure** para alterar o valor limite de custo do administrador de consultas em todo o servidor. Para obter mais informações sobre como configurar essa opção, consulte [sp_configure](../../relational-databases/system-stored-procedures/sp-configure-transact-sql.md) e [Opções de configuração do servidor &#40;SQL Server&#41;](../../database-engine/configure-windows/server-configuration-options-sql-server.md).  
  
 A configuração de SET QUERY_GOVERNOR_COST_LIMIT é definida no momento da execução e não no momento da análise.  
  
## <a name="permissions"></a>Permissões  
 Requer associação à função **pública** .  
  
## <a name="see-also"></a>Consulte Também  
 [Instruções SET &#40;Transact-SQL&#41;](../../t-sql/statements/set-statements-transact-sql.md)  
  
  
