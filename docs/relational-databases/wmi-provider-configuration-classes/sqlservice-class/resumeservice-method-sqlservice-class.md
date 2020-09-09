---
description: Método ResumeService (classe SqlService)
title: Método ResumeService (SqlService)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- ResumeService Method (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- ResumeService method
ms.assetid: 0b0a5f08-b95e-4626-bf81-309da7a0aacd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: b5c533cde7bccdbf198e207e6026beb0404f19cd
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542823"
---
# <a name="resumeservice-method-sqlservice-class"></a>Método ResumeService (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Tenta colocar o serviço no estado de reiniciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.ResumeService()  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32 , que é 0 se a solicitação **ResumeService** tiver sido aceita, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
