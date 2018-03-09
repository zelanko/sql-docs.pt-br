---
title: "Arquivos e números de versão | Microsoft Docs"
ms.custom: 
ms.date: 08/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: smo
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: a23f5abd57fdf723382671b82d6078cbb2c7b8d5
ms.sourcegitcommit: cb2f9d4db45bef37c04064a9493ac2c1d60f2c22
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/12/2018
---
# <a name="files-and-version-numbers"></a>Arquivos e números de versão
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Todos os necessários componentes do SQL Server Management Object (SMO) estão incluídos no pacote do Microsoft.SqlServer.SqlManagementObjects NuGet. SMO é implementado em vários assemblies gerenciados. Você pode desenvolver aplicativos SMO em um cliente ou um servidor.  

>>[!Important]
A versão do arquivo dos assemblies do SMO é exibida como principal. **0**. Build.Revision. Mas a versão de assembly inserido é o principal. **100**. Build.Revision. Isso é feito para manter a versão do SMO usado em todos os aplicativos separados para atualizações para um não afeta outras.
>>
>>Por isso, você deve **não** instalar essas versões dos assemblies para o Cache de Assembly Global (GAC). Isso pode fazer com que outros aplicativos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, para interromper. 
  
|Arquivo|Descrição|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contém suporte para conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contém suporte para programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Só é necessário em programas que acessam o Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contém o a maioria das classes SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contém suporte para as classes SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contém as classes de Provedor WMI (Windows Management Instrumentation). Só é necessário para programas que usam as classes de Provedor WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contém as classes de Servidor Registrado. Só é necessário para programas que usam as classes de Servidor Registrado.|  
  
  
