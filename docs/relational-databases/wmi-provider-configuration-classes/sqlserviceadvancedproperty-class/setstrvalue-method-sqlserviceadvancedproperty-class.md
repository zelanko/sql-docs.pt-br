---
title: Método SetStrValue (classe SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: reference
apiname:
- SetStrValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetStrValue method
ms.assetid: 1fededc3-81ba-4b08-83f9-189b96140799
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d77a40a4ebde6c034b2f9b5ff596a1819ccccfbb
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47747774"
---
# <a name="setstrvalue-method-sqlserviceadvancedproperty-class"></a>Método SetStrValue (classe SqlServiceAdvancedProperty)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Define o valor da cadeia de caracteres de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetStrValue(StrValue)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa uma propriedade avançada.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*strValue*|Um valor da cadeia de caracteres que especifica o valor da propriedade avançada.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
 O tipo de valor da propriedade deve ser *string* para definir a propriedade como um valor da cadeia de caracteres.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
