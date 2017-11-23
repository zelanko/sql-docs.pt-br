---
title: sp_wait_for_database_copy_sync (banco de dados do SQL Azure) | Microsoft Docs
ms.custom: 
ms.date: 03/03/2017
ms.prod: 
ms.prod_service: database-engine, sql-database
ms.reviewer: 
ms.service: sql-database
ms.component: system-stored-procedures
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs: TSQL
helpviewer_keywords: sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
caps.latest.revision: "13"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c7b2d41c9c87b483ab500ad351361a511ca66004
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="active-geo-replication---spwaitfordatabasecopysync"></a>Replicação geográfica ativa - sp_wait_for_database_copy_sync
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Este procedimento tem como escopo uma relação do [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] entre um banco de dados primário e um banco de dados secundário. Chamando o **sp_wait_for_database_copy_sync** faz com que o aplicativo espere até que todas as transações confirmadas sejam replicadas e reconhecidas pelo banco de dados secundário ativo. Executar **sp_wait_for_database_copy_sync** somente banco de dados primário.  
  
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
  
## <a name="remarks"></a>Comentários  
 Todas as transações confirmadas antes de um **sp_wait_for_database_copy_sync** chamada são enviadas para o banco de dados secundário ativo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir invoca **sp_wait_for_database_copy_sync** para garantir que todas as transações são confirmadas ao banco de dados primário, db0, sejam enviados ao seu banco de dados secundário ativo em ubfyu5ssyt de servidor de destino.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sys.DM continuous_copy_status &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [Funções e exibições de gerenciamento dinâmico de replicação geográfica &#40; Banco de dados SQL do Azure &#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)  
  
  
