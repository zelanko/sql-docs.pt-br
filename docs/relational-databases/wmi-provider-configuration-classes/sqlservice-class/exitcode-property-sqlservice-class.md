---
description: Propriedade ExitCode (classe SqlService)
title: Propriedade ExitCode (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ExitCode Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ExitCode property
ms.assetid: e6b8bff2-946f-4abe-bd50-1f7bb11fdddf
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 71e5fbe4180c67560709f004ba099bb90ca83b02
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542836"
---
# <a name="exitcode-property-sqlservice-class"></a>Propriedade ExitCode (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém ou define o código de erro Win32 do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] que define problemas encontrados quando o serviço é iniciado ou interrompido.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ExitCode [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** que especifica o código de saída.  
  
## <a name="remarks"></a>Comentários  
 Esta propriedade é definida como ERROR_SERVICE_SPECIFIC_ERROR (1066) quando o erro for exclusivo ao serviço representado por essa classe. O serviço define esse valor como NO_ERROR (0) quando está sendo executado e novamente, no encerramento normal.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
