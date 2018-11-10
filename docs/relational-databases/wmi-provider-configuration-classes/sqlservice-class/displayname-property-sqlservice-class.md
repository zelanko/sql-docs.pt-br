---
title: Propriedade DisplayName (classe SqlService) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- DisplayName Property (SqlService Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- DisplayName property
ms.assetid: 49c408aa-6eb4-45cd-8d5c-60f065f24f5c
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: 845df6c16993e7d570a12a2fa6f29ac4a781db49
ms.sourcegitcommit: 6c9d35d03c1c349bc82b9ed0878041d976b703c6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/06/2018
ms.locfileid: "51217844"
---
# <a name="displayname-property-sqlservice-class"></a>Propriedade DisplayName (classe SqlService)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]
  Obtém o nome para exibição do serviço.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.DisplayName [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe SqlService](../../../relational-databases/wmi-provider-configuration-classes/sqlservice-class/sqlservice-class.md) que representa o serviço.  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor da cadeia de caracteres que exibe o nome de host do serviço.  
  
## <a name="remarks"></a>Comentários  
 Essa cadeia de caracteres tem um tamanho máximo de 256 caracteres. O nome preserva a diferenciação de maiúsculas e minúsculas no Gerenciador de Configuração do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . No entanto, as comparações do nome para exibição nunca fazem diferenciação de maiúsculas e minúsculas.  
  
## <a name="example"></a>Exemplo  
  
```  
mysqlservice.DisplayName = "Atdisk"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Iniciando e parando serviços](http://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
