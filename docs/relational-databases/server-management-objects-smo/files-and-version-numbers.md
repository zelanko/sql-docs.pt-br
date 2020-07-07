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
author: markingmyname
ms.author: maghan
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 6d682ca3d6768da16d43c3c09471a6c722561dd3
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86008620"
---
# <a name="files-and-version-numbers"></a>Arquivos e números de versão
[!INCLUDE [SQL Server ASDB, ASDBMI, ASDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa.md)]

  Todos os componentes do SMO (objeto de gerenciamento de SQL Server) necessários estão incluídos no pacote NuGet Microsoft. SqlServer. SqlManagementObjects. SMO é implementado em vários assemblies gerenciados. Você pode desenvolver aplicativos SMO em um cliente ou um servidor.  

> > [!Important]
> > A versão do arquivo dos assemblies do SMO é exibida como principal. **0**. Build. Revision. Mas a versão de assembly inserida é a principal. **100**. Build. Revision. Isso é feito para manter a versão do SMO usada em cada aplicativo separadamente, de modo que as atualizações para uma não afetem as outras.
> > 
> > Por isso, você **não** deve instalar essas versões dos ASSEMBLIES no GAC (cache de assembly global). Isso pode fazer com que outros aplicativos, como [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Management Studio, sejam interrompidos. 
  
|Arquivo|Descrição|  
|-----------|-----------------|  
|Microsoft.SqlServer.ConnectionInfo.dll|Contém suporte para conexão a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|Microsoft.SqlServer.ServiceBrokerEnum.dll|Contém suporte para programação do [!INCLUDE[msCoName](../../includes/msconame-md.md)] Service Broker. Só é necessário em programas que acessam o Service Broker.|  
|Microsoft.SqlServer.Smo.dll|Contém o a maioria das classes SMO.|  
|Microsoft.SqlServer.SmoExtended.dll<br /><br /> Microsoft.SqlServer.Management.Sdk.Sfc.dll<br /><br /> Microsoft.SqlServer.SqlEnum.dll|Contém suporte para as classes SMO.|  
|Microsoft.SqlServer.WmiEnum.dll|Contém as classes de Provedor WMI (Windows Management Instrumentation). Só é necessário para programas que usam as classes de Provedor WMI.|  
|Microsoft.SqlServer.RegSvrEnum.dll|Contém as classes de Servidor Registrado. Só é necessário para programas que usam as classes de Servidor Registrado.|  
  
  
