---
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
ms.openlocfilehash: 4c4797b3452f64f7fee7a8d5653c13812d0af716
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85674137"
---
# <a name="catalogupdate_logdb_info-ssisdb-database"></a>catalog.update_logdb_info (Banco de Dados SSISDB)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/applies-to-version/sqlserver2017.md)]

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
 
