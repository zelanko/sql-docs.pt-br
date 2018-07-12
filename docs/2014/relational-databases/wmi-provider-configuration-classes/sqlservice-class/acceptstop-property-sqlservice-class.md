---
title: Propriedade AcceptStop (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- AcceptStop Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- AcceptStop property
ms.assetid: bf8ffe79-4f4c-4a2d-82e5-2ae8f5d466c5
caps.latest.revision: 35
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 7ee6991565a78ddf4b0b76d82d30ebd0da0892c9
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37228758"
---
# <a name="acceptstop-property-sqlservice-class"></a>Propriedade AcceptStop (classe SqlService)
  Obtém o valor da propriedade booliana que especifica se o serviço pode ser interrompido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.AcceptStop [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um [SqlService classe](sqlservice-class.md) objeto que representa o serviço  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se o serviço pode ser interrompido. `true` se o serviço puder interrompido; `false` se o serviço não puder ser interrompido.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
