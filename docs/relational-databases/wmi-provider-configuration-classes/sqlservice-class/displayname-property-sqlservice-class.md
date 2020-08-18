---
description: Propriedade DisplayName (classe SqlService)
title: Propriedade DisplayName (SqlService)
ms.custom: seo-lt-2019
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
ms.openlocfilehash: a1180c25be8d081d39fed1cc13926391289e5c30
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88472698"
---
# <a name="displayname-property-sqlservice-class"></a>Propriedade DisplayName (classe SqlService)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
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
  
## <a name="see-also"></a>Consulte Também  
 [Iniciando e parando serviços](https://technet.microsoft.com/library/ms174886\(v=sql.105\).aspx)  
  
  
