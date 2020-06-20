---
title: Propriedade ExitCode (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f7f5414afd8507a1fc9c592d6b8226692e9683a0
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002196"
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
  
## <a name="remarks"></a>Comentários  
 Esta propriedade é definida como ERROR_SERVICE_SPECIFIC_ERROR (1066) quando o erro for exclusivo ao serviço representado por essa classe. O serviço define esse valor como NO_ERROR (0) quando está sendo executado e novamente, no encerramento normal.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
