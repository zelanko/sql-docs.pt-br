---
description: Replicação geográfica ativa-sp_wait_for_database_copy_sync
title: sp_wait_for_database_copy_sync
titleSuffix: Azure SQL Database
ms.date: 03/03/2017
ms.service: sql-database
ms.reviewer: ''
ms.topic: language-reference
f1_keywords:
- sp_wait_for_database_copy_sync_TSQL
- sp_wait_for_database_copy_sync
dev_langs:
- TSQL
helpviewer_keywords:
- sp_wait_for_database_copy_sync
ms.assetid: 7068da7f-cb74-47f2-b064-eb076a0d3885
author: CarlRabeler
ms.author: carlrab
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.custom: seo-dt-2019
ms.openlocfilehash: eb1ac50e4da538d80e743114714fe216d35a89fc
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88481601"
---
# <a name="active-geo-replication---sp_wait_for_database_copy_sync"></a>Replicação geográfica ativa-sp_wait_for_database_copy_sync
[!INCLUDE[Azure SQL Database Azure SQL Managed Instance](../../includes/applies-to-version/asdb-asdbmi.md)]

  Este procedimento tem como escopo uma relação do [!INCLUDE[ssGeoDR](../../includes/ssgeodr-md.md)] entre um banco de dados primário e um banco de dados secundário. Chamar o **sp_wait_for_database_copy_sync** faz com que o aplicativo aguarde até que todas as transações confirmadas sejam replicadas e confirmadas pelo banco de dados secundário ativo. Execute **sp_wait_for_database_copy_sync** somente no banco de dados primário.  
  
||  
|-|  
|**Aplica-se a**: [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)].|  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_wait_for_database_copy_sync [ @target_server = ] 'server_name'   
     , [ @target_database = ] 'database_name'  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @target_server =] ' server_name '  
 O nome do servidor do Banco de Dados SQL que hospeda o banco de dados secundário ativo. server_name é sysname, sem padrão.  
  
 [ @target_database = ] 'database_name'  
 O nome do banco de dados secundário ativo. database_name é sysname, sem padrão.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 Retorna 0 para êxito ou um número de erro para falha.  
  
 As condições de erro mais prováveis são as seguintes:  
  
-   O nome do servidor ou do banco de dados está ausente.  
  
-   O link não pode ser localizado no nome do servidor ou banco de dados especificado.  
  
-   A conectividade do interlink é perdida. **sp_wait_for_database_copy_sync** retornará após o tempo limite de conexão.  
  
## <a name="permissions"></a>Permissões  
 Qualquer usuário no banco de dados primário pode chamar este procedimento armazenado do sistema. O logon deve ser um usuário nos bancos de dados primário e secundário ativo.  
  
## <a name="remarks"></a>Comentários  
 Todas as transações confirmadas antes de uma chamada de **sp_wait_for_database_copy_sync** são enviadas para o banco de dados secundário ativo.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir invoca **sp_wait_for_database_copy_sync** para garantir que todas as transações sejam confirmadas no banco de dados primário, db0, sejam enviadas para seu banco de dados secundário ativo no servidor de destino ubfyu5ssyt.  
  
```  
USE db0;  
GO  
EXEC sys.sp_wait_for_database_copy_sync @target_server = N'ubfyu5ssyt1', @target_database = N'db0';  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [sys. dm_continuous_copy_status &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-continuous-copy-status-azure-sql-database.md)   
 [DMVs (exibições de gerenciamento dinâmico) de replicação geográfica e funções &#40;banco de dados SQL do Azure&#41;](../../relational-databases/system-dynamic-management-views/geo-replication-dynamic-management-views-and-functions-azure-sql-database.md)   
 [sys.dm_geo_replication_link_status](../system-dynamic-management-views/sys-dm-geo-replication-link-status-azure-sql-database.md)
  
  
