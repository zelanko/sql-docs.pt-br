---
title: Arquivos e números de versão | Microsoft Docs
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
helpviewer_keywords:
- SQL Server Management Objects, versions
- components [SMO]
- files [SMO], components
- SMO [SQL Server], versions
- versions [SMO]
ms.assetid: 510907b6-e7a9-41bd-b892-d6d99a5118e1
caps.latest.revision: 32
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 63602af6a7d798086c3e41d3796b20a2f71d6950
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36122807"
---
# <a name="files-and-version-numbers"></a>Arquivos e números de versão
  Todos os necessário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Objects (SMO) componentes são instalados como parte de uma instância de [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cliente ou servidor. SMO é implementado em vários assemblies gerenciados. Você pode desenvolver aplicativos SMO em um cliente ou um servidor.  
  
|Diretório|Arquivo|Description|  
|---------------|----------|-----------------|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ConnectionInfo.dll|Contém suporte para conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contém suporte para programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Só é necessário em programas que acessam o Service Broker.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.Smo.dll|Contém o a maioria das classes SMO.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contém suporte para as classes SMO.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.WmiEnum.dll|Contém as classes de Provedor WMI (Windows Management Instrumentation). Só é necessário para programas que usam as classes de Provedor WMI.|  
|[!INCLUDE[ssSampPathSDK](../../includes/sssamppathsdk-md.md)]|Microsoft.SqlServer.RegSvrEnum.dll|Contém as classes de Servidor Registrado. Só é necessário para programas que usam as classes de Servidor Registrado.|  
  
  