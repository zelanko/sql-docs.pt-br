---
title: Método SetStrValue (classe SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStrValue Method (SqlServiceAdvancedProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStrValue method
ms.assetid: 1fededc3-81ba-4b08-83f9-189b96140799
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: d8cb4bb7aec53ebc28a91cc36add1ae810b08d44
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62911840"
---
# <a name="setstrvalue-method-sqlserviceadvancedproperty-class"></a>Método SetStrValue (classe SqlServiceAdvancedProperty)
  Define o valor da cadeia de caracteres de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetStrValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServiceAdvancedProperty](sqlserviceadvancedproperty-class.md) que representa uma propriedade avançada.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*StrValue*|Um valor da cadeia de caracteres que especifica o valor da propriedade avançada.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
 O tipo de valor da propriedade deve ser *string* para definir a propriedade como um valor da cadeia de caracteres.  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
