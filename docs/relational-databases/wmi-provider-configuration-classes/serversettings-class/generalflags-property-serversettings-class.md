---
description: Propriedade GeneralFlags (classe ServerSettings)
title: Propriedade GeneralFlags (ServerSettings)
ms.custom: seo-lt-2019
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: wmi
ms.topic: reference
apiname:
- GeneralFlags Property (ServerSettings Class)
apilocation:
- sqlmgmproviderxpsp2up.mof
apitype: MOFDef
helpviewer_keywords:
- GeneralFlags property
ms.assetid: 129bff8d-d2bc-4297-952f-d0a919d169f7
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 75f871ee6734fbd70316209fbac02841b0c3a6f4
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89522412"
---
# <a name="generalflags-property-serversettings-class"></a>Propriedade GeneralFlags (classe ServerSettings)
[!INCLUDE [SQL Server](../../../includes/applies-to-version/sqlserver.md)]
  Obtém os sinalizadores gerais associados à instância do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
object.GeneralFlags [= value]  
```  
  
## <a name="parts"></a>Partes  
 *object*  
 Um objeto da [classe ServerSettings](../../../relational-databases/wmi-provider-configuration-classes/serversettings-class/serversettings-class.md) que representa as configurações de servidor em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="property-valuereturn-value"></a>Valor da propriedade/Valor do retorno  
 Uma matriz de objetos da [classe ServerSettingsGeneralFlag](../../../relational-databases/wmi-provider-configuration-classes/serversettingsgeneralflag-class/serversettingsgeneralflag-class.md) que especificam os sinalizadores gerais associados com a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
## <a name="remarks"></a>Comentários  
  
## <a name="see-also"></a>Consulte Também  
 [Configurando protocolos de rede de servidor e Net-Libraries](https://msdn.microsoft.com/library/ms177485\(v=sql.100\).aspx)  
  
  
