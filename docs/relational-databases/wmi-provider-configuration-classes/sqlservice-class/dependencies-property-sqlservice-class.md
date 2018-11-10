---
title: Propriedade Dependencies (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- Dependencies Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- Dependencies property
ms.assetid: 92d54b7e-de2f-4978-b601-0196e37cbb41
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 1c2ae0553627e80daf99a7bd23fe1182f5df52d2
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217894"
---
# <a name="dependencies-property-sqlservice-class"></a>Propriedade Dependencies (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém uma lista de serviços que são dependentes do serviço referenciado.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.Dependencies [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz da cadeia de caracteres[] que contém uma lista de serviços dependentes do serviço referenciado.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
