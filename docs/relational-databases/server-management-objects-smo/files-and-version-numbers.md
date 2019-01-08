---
title: Arquivos e números de versão | Microsoft Docs
ms.custom: ''
ms.date: 08/06/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
author: stevestein
ms.author: sstein
manager: craigg
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 0a72b776add3dc1fb31886711b3f812b65d1176c
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53203696"
---
# <a name="files-and-version-numbers"></a>Arquivos e números de versão
[!INCLUDE[appliesto-ss-asdb-asdw-xxx-md](../../includes/appliesto-ss-asdb-asdw-xxx-md.md)]

  Todos os necessários componentes do SQL Server Management Object (SMO) estão incluídos no pacote Microsoft.SqlServer.SqlManagementObjects NuGet. SMO é implementado em vários assemblies gerenciados. Você pode desenvolver aplicativos SMO em um cliente ou um servidor.  

> > [!Important]
> > A versão dos assemblies SMO é exibida como principal. **0**. Build.Revision. Mas a versão do assembly inserido é o principal. **100**. Build.Revision. Isso é feito para manter a versão do SMO usado em cada aplicativo separado para que as atualizações para um não afetam todos os outros.
> > 
> > Por isso você deve **não** instalar essas versões de assemblies ao Cache de Assembly Global (GAC). Isso poderia fazer com que outros aplicativos, tais como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, a fim de interromper. 
  
|Arquivo|Descrição|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contém suporte para conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contém suporte para programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Só é necessário em programas que acessam o Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contém o a maioria das classes SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contém suporte para as classes SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contém as classes de Provedor WMI (Windows Management Instrumentation). Só é necessário para programas que usam as classes de Provedor WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contém as classes de Servidor Registrado. Só é necessário para programas que usam as classes de Servidor Registrado.|  
  
  
