---
title: Propriedade State (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- State Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cc1484a09929f4e4a8534b2c2acac2089adfbb97
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62912181"
---
# <a name="state-property-sqlservice-class"></a>Propriedade State (classe SqlService)
  Obtém ou define o estado atual do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.State [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 que especifica o estado do serviço.  
  
 Pode conter um dos valores a seguir.  
  
 1  
 Stopped. O serviço foi interrompido.  
  
 2  
 Start Pending. O serviço está aguardando para iniciar.  
  
 3  
 Stop Pending. O serviço está aguardando paras ser interrompido.  
  
 4  
 Running. O serviço está sendo executado.  
  
 5  
 Continue Pending. O serviço está aguardando para prosseguir.  
  
 6  
 Pause Pending. O serviço está aguardando para ser pausado.  
  
 7  
 Em pausa. O serviço foi pausado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
