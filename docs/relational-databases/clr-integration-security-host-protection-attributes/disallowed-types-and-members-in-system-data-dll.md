---
description: Tipos e membros não permitidos em System.Data.dll
title: Tipos e membros não permitidos em System.Data.dll | Microsoft Docs
descriptions: SQL Server CLR programming disallows a type or member with some values for the HostProtectionResource enum. This article lists System.Data.dll disallowed values.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
ms.openlocfilehash: 02c659d599491a61a42784a09d0e68a25b44c73a
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429018"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos e membros não permitidos em System.Data.dll
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a programação comum de integração de linguagem (CLR) não permite o uso de um tipo ou membro que tenha um **HostProtectionAttribute** que especifique uma enumeração **System. Security. Permissions. HostProtectionResource** com um valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**ou **UI**. A tabela a seguir lista os membros e os tipos do assembly System.Data.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo ou membro|Valor(es) de HPA|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery ()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Sincronização|  
|System.Xml.XmlDataDocument|Sincronização|  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos de proteção do host e programação de integração CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos e membros não permitidos em Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos e membros não permitidos em mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos e membros não permitidos em System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros desaprovados no System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
