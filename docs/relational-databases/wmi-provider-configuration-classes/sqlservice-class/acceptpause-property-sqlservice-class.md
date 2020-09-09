---
description: Propriedade AcceptPause (classe SqlService)
title: Propriedade AcceptPause (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- AcceptPause Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
helpviewer_keywords:
- AcceptPause property
ms.assetid: 4339e903-35ee-4395-b005-ca58b3a24a84
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 5b86054eb6ce914a094f537374611ff71180f156
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89550872"
---
# <a name="acceptpause-property-sqlservice-class"></a>Propriedade AcceptPause (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém o valor da propriedade booliana que especifica se o serviço pode ser pausado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.AcceptPause [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se é possível pausar o serviço. **true** se for possível pausar o serviço; **false** se não for possível pausar o serviço.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
