---
title: Classe ProcessId (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- ProcessId Class (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ProcessId property
ms.assetid: 99b5a2e9-b44a-48a0-993e-04bd15c7fef4
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b9e6c04a0ae0000284f3550d39e47c973adbe8ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63061914"
---
# <a name="processid-class-sqlservice-class"></a>Classe ProcessId (classe SqlService)
  Obtém a ID de processo de sistema que identifica exclusivamente um serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.ProcessId [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32` que especifica a ID que identifica exclusivamente o processo.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="example"></a>Exemplo  
  
```  
mysqlservice.ProcessId = 324  
```  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
