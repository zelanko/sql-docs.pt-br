---
title: Método GetCurrentCertificate (classe SInstance) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- GetCurrentCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- GetCurrentCertificate method
ms.assetid: 9d2b72df-cb21-414a-abef-917f13d4de62
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 75b383d6e983f035b22a6b6949d0c640b17007fd
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37270342"
---
# <a name="getcurrentcertificate-method-sinstance-class"></a>Método GetCurrentCertificate (classe SInstance)
  Obtém o certificado de segurança atual.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.GetCurrentCertificate(  
SHA  
)  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SInstance](sinstance-class.md) que representa as configurações de servidor em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Description|  
|---------------|-----------------|  
|*SHA*|Um valor de objeto da cadeia de caracteres (parâmetro de saída) que especifica o certificado de segurança atual depois que o método é concluído.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor `uint32`, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
