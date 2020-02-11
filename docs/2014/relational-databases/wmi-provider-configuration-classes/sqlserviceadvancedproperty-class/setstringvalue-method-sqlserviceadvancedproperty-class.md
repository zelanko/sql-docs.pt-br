---
title: Método SetStringValue (classe SqlServiceAdvancedProperty) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- SetStringValue Method (SqlServiceAdvancedProperty Class )
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- SetStringValue method
ms.assetid: a02d05f6-1072-4709-9ecc-e23e51c8c898
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: b0209f3d8e77cfe893a0e462fc9ccf3761da8dfa
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62911388"
---
# <a name="setstringvalue-method-sqlserviceadvancedproperty-class-"></a>Método SetStringValue (classe SqlServiceAdvancedProperty)
  Define o valor da cadeia de caracteres de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.SetStringValue(  
StrValue  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlServiceAdvancedProperty](sqlserviceadvancedproperty-class.md) que representa uma propriedade avançada.  
  
#### <a name="parameters"></a>parâmetros  
  
|Parâmetro|DESCRIÇÃO|  
|---------------|-----------------|  
|*StrValue*|Um valor da cadeia de caracteres que especifica o valor da propriedade avançada.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
 O tipo de valor da propriedade deve ser `string` para definir a propriedade como um valor da cadeia de caracteres.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
