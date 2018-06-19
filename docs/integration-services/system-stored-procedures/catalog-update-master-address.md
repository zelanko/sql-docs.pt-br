---
title: catalog.update_master_address (banco de dados SSISDB) | Microsoft Docs
ms.custom: ''
ms.date: 07/18/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: language-reference
caps.latest.revision: 1
author: haoqian
ms.author: haoqian
manager: craigg
monikerRange: '>= sql-server-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: 50953f913101cf4ec08bf492034abb1d5e43da40
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35406918"
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
 
