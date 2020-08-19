---
description: catalog.update_logdb_info (Banco de Dados SSISDB)
title: catalog.update_logdb_info (Banco de Dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: language-reference
author: haoqian
ms.author: haoqian
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 78a720f0ac29337dd7752fc72fe93ea3a3f91018
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88495359"
---
# <a name="catalogupdate_logdb_info-ssisdb-database"></a>catalog.update_logdb_info (Banco de Dados SSISDB)

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


[!INCLUDE[sqlserver2017](../../includes/applies-to-version/sqlserver2017.md)]

Atualize as informações de log do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out.

## <a name="syntax"></a>Sintaxe

```sql
catalog.update_logdb_info [ @server_name = ] server_name, [ @connection_string = ] connection_string
```

## <a name="arguments"></a>Argumentos
[ @server_name = ] *server_name*  
 O SQL Server usado para log do Scale Out. O *server_name* é **nvarchar**.  

 [ @connection_string = ] *connection_string*  
 A cadeia de conexão usada para registro em log do Scale Out. O *connection_string* é **nvarchar**.

 ## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
   
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
 
