---
title: Método RemoveCertificate (classe SInstance) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
api_name:
- RemoveCertificate Method (SInstance Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- RemoveCertificate method
ms.assetid: 7e5dbafa-a634-4617-9622-510514fce0ce
caps.latest.revision: 14
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 56fcc69e20517602e906057f411d97fbaa7191e1
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37258492"
---
# <a name="removecertificate-method-sinstance-class"></a>Método RemoveCertificate (classe SInstance)
  Remove o certificado de segurança atual da instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.RemoveCertificate()  
  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SInstance](sinstance-class.md) que representa as configurações de servidor em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor uint32, que é 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Remarks  
  
## <a name="see-also"></a>Consulte também  
 [Configurando protocolos de rede do servidor e bibliotecas de rede](http://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
