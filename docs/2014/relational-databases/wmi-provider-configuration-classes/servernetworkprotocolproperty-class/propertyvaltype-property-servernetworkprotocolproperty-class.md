---
title: Propriedade PropertyValType (classe ServerNetworkProtocolProperty) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- PropertyValType Property (ServerNetworkProtocolProperty Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- PropertyValType property
ms.assetid: fbd42e8e-0642-4a19-b3c8-6ce88345145f
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: be6c42fbaa36080ec8144d95abb045a3b4328057
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85002498"
---
# <a name="propertyvaltype-property-servernetworkprotocolproperty-class"></a>Propriedade PropertyValType (classe ServerNetworkProtocolProperty)
  Obtém o tipo de dados do valor armazenado na propriedade referenciada.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.PropertyValType [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 A [classe ServerNetworkProtocolProperty](servernetworkprotocolproperty-class.md) que representa um atributo do protocolo de rede na instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32` que especifica o tipo de dado do valor da propriedade. Retorna 0 para um valor da cadeia de caracteres e 1 para um tipo numérico.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
