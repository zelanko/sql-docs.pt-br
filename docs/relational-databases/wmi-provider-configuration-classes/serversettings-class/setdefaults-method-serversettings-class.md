---
description: Método SetDefaults (classe ServerSettings)
title: Método SetDefaults (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- SetDefaults Method (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- SetDefaults method
ms.assetid: 76e4cfab-4b15-4da4-bb2f-8aac6f927f79
author: markingmyname
ms.author: maghan
ms.openlocfilehash: e9829b6f477fb385f59b312c0e1e9f9feb65fb31
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89544287"
---
# <a name="setdefaults-method-serversettings-class"></a>Método SetDefaults (classe ServerSettings)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Define todos os valores padrão para a instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] com a opção de substituir os dados existentes.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.SetDefaults(OverwriteAll)  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto de [classe ServerSettings](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) que representa uma [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância de cliente.  
  
#### <a name="parameters"></a>Parâmetros  
  
|Parâmetro|Descrição|  
|---------------|-----------------|  
|*OverwriteAll*|Um valor booliano que especifica se os valores existentes devem ser substituídos na instância de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] : **true** para substituir os dados existentes ou **false** se os dados existentes não forem substituídos.|  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Um valor u**Int32** , que será 0 se o serviço tiver sido modificado com êxito, 1 se a solicitação não tiver suporte e qualquer outro número para indicar um erro.  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
