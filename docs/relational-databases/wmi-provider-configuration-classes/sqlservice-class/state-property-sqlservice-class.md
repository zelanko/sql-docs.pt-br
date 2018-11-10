---
title: Estado de propriedade (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- State Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- State property
ms.assetid: 9e09f419-947c-4d4b-9a49-2d3396c847cd
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b7351f0b341a652ff7616bde788581caa087a7e9
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51216024"
---
# <a name="state-property-sqlservice-class"></a>Propriedade State (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém ou define o estado atual do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
