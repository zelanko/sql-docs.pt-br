---
title: sp_wait_for_database_copy_sync (banco de dados SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: ''
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: system-objects
ms.tgt_pltfrm: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: 13
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: bb228500b59252898bbe25cf377b87b62b754860
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43104367"
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Replicação geográfica ativa - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este procedimento tem como escopo uma relação do [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] entre um banco de dados primário e um banco de dados secundário. Chamar o **sp_wait_for_database_copy_sync** faz com que o aplicativo espere até que todas as transações confirmadas sejam replicadas e reconhecidas pelo banco de dados secundário ativo. Execute **sp_wait_for_database_copy_sync** somente banco de dados primário.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @target_server =] 'server_name'  
 O nome do servidor do Banco de Dados SQL que hospeda o banco de dados secundário ativo. server_name é sysname, sem padrão.  
  
 [ @target_database =] 'database_name'  
 O nome do banco de dados secundário ativo. database_name é sysname, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Retorna 0 para êxito ou um número de erro para falha.  
  
 As condições de erro mais prováveis são as seguintes:  
  
-   O nome do servidor ou do banco de dados está ausente.  
  
-   O link não pode ser localizado no nome do servidor ou banco de dados especificado.  
  
-   A conectividade do interlink é perdida. **sp_wait_for_database_copy_sync** será retornado após o tempo limite da conexão.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário no banco de dados primário pode chamar este procedimento armazenado do sistema. O logon deve ser um usuário nos bancos de dados primário e secundário ativo.  
  
## <a name="remarks"></a>Remarks  
 Todas as transações confirmadas antes de uma **sp_wait_for_database_copy_sync** chamada são enviadas para o banco de dados secundário ativo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir invoca **sp_wait_for_database_copy_sync** para garantir que todas as transações são confirmadas no banco de dados primário, db0, sejam enviadas ao seu banco de dados secundário ativo em ubfyu5ssyt de servidor de destino.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.dm_continuous_copy_status &#40;banco de dados SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Funções e exibições de gerenciamento dinâmico de replicação geográfica &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
