---
title: catalog.update_master_address (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
ms.workload: Inactive
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ee47c3bbd6d0e8f29152ca0869b3315855180a0f
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="catalogupdatemasteraddress-ssisdb-database"></a>catalog.update_master_address (banco de dados SSISDB)
[!INCLUDE[tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md](../../includes/tsql-appliesto-ss2017-xxxx-xxxx-xxx-md.md)]

Atualize o ponto de extremidade do Mestre do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] Scale Out.

## <a name="syntax"></a>Sintaxe

```sql
catalog.update_master_address [@MasterAddress = ] masterAddress
```

## <a name="arguments"></a>Argumentos
[ @MasterAddress = ] *masterAddress*  
O ponto de extremidade do Mestre do Scale Out. O *masterAddress* é **nvarchar**.  

 ## <a name="return-code-value"></a>Valor do código de retorno  
 0 (êxito)  
  
## <a name="result-sets"></a>Conjuntos de resultados  
 Nenhum  

## <a name="permissions"></a>Permissões  
 Este procedimento armazenado exige uma das seguintes permissões:  
   
-   Associação à função de banco de dados **ssis_admin**  
  
-   Associação à função de servidor **sysadmin**  
 
