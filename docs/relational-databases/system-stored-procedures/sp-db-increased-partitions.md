---
title: sp_db_increased_partitions | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs:
- TSQL
helpviewer_keywords:
- sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 73f3eca2a2e7943d8911144a3657e4f826d9739c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62506723"
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita ou desabilita suporte para até 15.000 partições para o banco de dados especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname= ] '*database_name*'  
 É o nome do banco de dados. *DBName* está **sysname** com um valor padrão de NULL. Se *dbname* não for especificado, o banco de dados atual será usado.  
  
 [ @increased_partitions= ] '*increased_partitions*'  
 Habilita ou desabilita suporte para 15.000 partições no banco de dados especificado. *increased_partitions* está **varchar(6)** com um padrão NULL. Os valores aceitos são 'ON' ou 'TRUE' para habilitar suporte e 'OFF' ou 'FALSE' para desabilitar o suporte. Se *increased_partitions* não for especificado, o procedimento retornará 1 para indicar o suporte está habilitado para o banco de dados especificado ou 0 para indicar o suporte está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER DATABASE no banco de dados especificado.  
  
  
