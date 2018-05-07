---
title: Propriedade AliasName (classe SqlServerAlias) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.component: wmi
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: reference
apiname:
- AliasName Property (SqlServerAlias Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AliasName property
ms.assetid: 5c4c88f3-c1cf-471a-9d91-f47657933e2f
caps.latest.revision: 31
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 3929b1aea1cd0008d0c7c5ec94ce909c7a2b40fb
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="aliasname-property-sqlserveralias-class"></a>Propriedade AliasName (classe SqlServerAlias)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém o nome do alias de conexão do servidor.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.AliasName [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlServerAlias](../../../relational-databases/wmi-provider-configuration-classes/sqlserveralias-class/sqlserveralias-class.md) que representa um alias do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **string** que especifica o nome do alias de conexão do servidor.  
  
## <a name="remarks"></a>Remarks  
  
