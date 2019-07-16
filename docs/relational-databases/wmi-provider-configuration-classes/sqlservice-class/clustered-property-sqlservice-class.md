---
title: Clustered (classe SqlService) de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Clustered Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 5052595dc30d0cb0959728f36f3e96acf96ab97d
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67929917"
---
# <a name="clustered-property-sqlservice-class"></a>Propriedade Clustered (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém o valor booliano da propriedade que especifica se o serviço é parte de uma instância em cluster.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Clustered [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/valor de retorno  
 Um valor booliano que especifica se o serviço está participando de uma instância em cluster: **true** se o serviço estiver participando de uma instância em cluster ou **false** se o serviço não estiver participando de uma instância em cluster.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
