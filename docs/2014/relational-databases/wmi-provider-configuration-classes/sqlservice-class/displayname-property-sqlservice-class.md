---
title: Propriedade DisplayName (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
api_name:
- DisplayName Property (SqlService Class)
api_location:
- sqlmgmproviderxpsp2up.mof
topic_type:
- apiref
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: cb5a00278e8b740df5efa93e71c417ccb4943f5d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63016298"
---
# <a name="displayname-property-sqlservice-class"></a>Propriedade DisplayName (classe SqlService)
  Obtém o nome para exibição do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object  
.DisplayName [= value]  
```  
  
## <a name="parts"></a>Partes  
 *objeto*  
 Um objeto da [classe SqlService](sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor da cadeia de caracteres que exibe o nome de host do serviço.  
  
## <a name="remarks"></a>Comentários  
 Essa cadeia de caracteres tem um tamanho máximo de 256 caracteres. O nome preserva a diferenciação de maiúsculas e minúsculas no Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . No entanto, as comparações do nome para exibição nunca fazem diferenciação de maiúsculas e minúsculas.  
  
## <a name="example"></a>Exemplo  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
