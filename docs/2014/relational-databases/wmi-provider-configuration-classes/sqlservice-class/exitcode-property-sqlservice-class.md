---
title: Propriedade ExitCode (classe SqlService) | Microsoft Docs
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
- ExitCode Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
caps.latest.revision: 34
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 33f4f09edd36381cb5ecf4768caeef9ac7b495bc
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37191656"
---
# <a name="exitcode-property-sqlservice-class"></a>Propriedade ExitCode (classe SqlService)
  Obtém ou define o código de erro Win32 do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que define problemas encontrados quando o serviço é iniciado ou interrompido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.ExitCode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32` que especifica o código de saída.  
  
## <a name="remarks"></a>Remarks  
 Esta propriedade é definida como ERROR_SERVICE_SPECIFIC_ERROR (1066) quando o erro for exclusivo ao serviço representado por essa classe. O serviço define esse valor como NO_ERROR (0) quando está sendo executado e novamente, no encerramento normal.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
