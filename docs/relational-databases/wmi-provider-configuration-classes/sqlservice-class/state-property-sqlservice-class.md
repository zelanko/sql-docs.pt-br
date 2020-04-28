---
title: Propriedade de estado (SqlService)
ms.custom: seo-lt-2019
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
ms.openlocfilehash: fbccc720f30bd98660e48d7c82a132f76dcf1a26
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "73660851"
---
# <a name="state-property-sqlservice-class"></a>Propriedade State (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém ou define o estado atual do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.State [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
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
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
