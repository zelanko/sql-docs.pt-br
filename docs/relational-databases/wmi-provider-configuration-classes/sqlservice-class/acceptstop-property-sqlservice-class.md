---
title: Propriedade AcceptStop (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptStop Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 324df0e451fd2fbdc2986c5f0bc4add86f90eabe
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217324"
---
# <a name="acceptstop-property-sqlservice-class"></a>Propriedade AcceptStop (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém o valor da propriedade booliana que especifica se o serviço pode ser interrompido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.AcceptStop [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um [SqlService classe](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) objeto que representa o serviço  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se o serviço pode ser interrompido: **verdadeira** se o serviço pode ser interrompido, ou **falso** se o serviço não pode ser interrompido.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
