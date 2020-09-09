---
description: Método SetNumericalValue (classe SqlServiceAdvancedProperty)
title: Método SetNumericalValue (SqlServiceAdvancedProperty)
ms.custom: seo-lt-2019
ms.date: 03/04/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetNumericalValue Method (SqlServiceAdvancedProperty Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetNumericalValue method
ms.assetid: 950ed1e8-0538-4db4-807c-a2c36f43cf6b
author: markingmyname
ms.author: maghan
ms.openlocfilehash: a3c9ccf43a8edd0298de5d9d7ecbcfbbcfea3c5e
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89542747"
---
# <a name="setnumericalvalue-method-sqlserviceadvancedproperty-class"></a>Método SetNumericalValue (classe SqlServiceAdvancedProperty)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Define o valor numérico de uma propriedade.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetNumericalValue(NumValue)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlServiceAdvancedProperty](../../../relational-databases/wmi-provider-configuration-classes/sqlserviceadvancedproperty-class/sqlserviceadvancedproperty-class.md) que representa uma propriedade avançada.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*NumValue*|Um valor **uint32** que especifica o valor da propriedade avançada.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor **uint32** , que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
 O tipo de valor da propriedade deve ser numérico para poder definir a propriedade como um valor numérico.  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
