---
title: Clustered (classe SqlService) de propriedade | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
api_name:
- Clustered Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- Clustered property
ms.assetid: f714e7f5-c2db-45c6-9536-6ca2cb5b42aa
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 58ca448090841c06d208c64f6ff483cc5cdb8473
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48079897"
---
# <a name="clustered-property-sqlservice-class"></a>Propriedade Clustered (classe SqlService)
  Obtém o valor booliano da propriedade que especifica se o serviço é parte de uma instância em cluster.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.Clustered [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor booliano que especifica se o serviço está participando de uma instância em cluster: `true` se o serviço estiver participando de uma instância em cluster ou `false` se o serviço não estiver participando de uma instância em cluster.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
