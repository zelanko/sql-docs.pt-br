---
title: sp_db_increased_partitions | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
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
- sp_db_increased_partitions_TSQL
- sp_db_increased_partitions
dev_langs: TSQL
helpviewer_keywords: sp_db_increased_partitions
ms.assetid: a8c043ec-b504-4929-ac0e-8babaa99d989
caps.latest.revision: "9"
author: edmacauley
ms.author: edmaca
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5266ce8c25465b6fd398111e7fd7e2d6634f5f34
ms.sourcegitcommit: 45e4efb7aa828578fe9eb7743a1a3526da719555
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/21/2017
---
# <a name="spdbincreasedpartitions"></a>sp_db_increased_partitions
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Habilita ou desabilita suporte para até 15.000 partições para o banco de dados especificado.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ([!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)] SP2 por meio de [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] SP1 e versões posteriores). Para obter mais informações, consulte [suporte para 15.000 partições no SQL Server 2008 SP2 e SQL Server 2008 R2 SP1](http://go.microsoft.com/fwlink/p/?LinkId=299658),|  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_dp_increased_partitions   
[ @dbname ] = 'database_name'   
[ , [ @increased_partitions = ] 'increased_partitions' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname=] '*database_name*'  
 É o nome do banco de dados. *DBName* é **sysname** com um valor padrão de NULL. Se *dbname* não for especificado, o banco de dados atual será usado.  
  
 [ @increased_partitions=] '*increased_partitions*'  
 Habilita ou desabilita suporte para 15.000 partições no banco de dados especificado. *increased_partitions* é **varchar(6)** com um padrão NULL. Os valores aceitos são 'ON' ou 'TRUE' para habilitar suporte e 'OFF' ou 'FALSE' para desabilitar o suporte. Se *increased_partitions* não for especificado, o procedimento retornará 1 para indicar o suporte está habilitado para o banco de dados especificado ou 0 para indicar o suporte está desabilitado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="permissions"></a>Permissões  
 Requer permissão ALTER DATABASE no banco de dados especificado.  
  
  
