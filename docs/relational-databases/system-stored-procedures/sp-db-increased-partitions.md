---
description: sp_db_increased_partitions
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 0cac6cc79f06087b7ddd79dcd891ad370ad1338f
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89536598"
---
# <a name="sp_db_increased_partitions"></a>sp_db_increased_partitions
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Habilita ou desabilita suporte para até 15.000 partições para o banco de dados especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname =] '*database_name*'  
 É o nome do banco de dados. *dbname* é **sysname** com um valor padrão de NULL. Se *dbname* não for especificado, o banco de dados atual será usado.  
  
 [ @increased_partitions =] '*increased_partitions*'  
 Habilita ou desabilita suporte para 15.000 partições no banco de dados especificado. *increased_partitions* é **varchar (6)** com um padrão de NULL. Os valores aceitos são 'ON' ou 'TRUE' para habilitar suporte e 'OFF' ou 'FALSE' para desabilitar o suporte. Se *increased_partitions* não for especificado, o procedimento retornará 1 para indicar que o suporte está habilitado para o banco de dados especificado ou 0 para indicar que o suporte está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER DATABASE no banco de dados especificado.  
  
  
