---
title: Tipos e membros não permitidos em System. Data. dll | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 4233bc1ddd98d6fe678d9d37f1acd7a4b66b687e
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874366"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos e membros não permitidos em System.Data.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]a programação comum de integração de linguagem (CLR) não permite o uso de um tipo ou membro que `HostProtectionAttribute` tenha um que `System.Security.Permissions.HostProtectionResource` especifique uma enumeração com um `ExternalProcessMgmt`valor `ExternalThreading`de `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, **SharedState**,, `Synchronization`SharedState, `UI`ou. A tabela a seguir lista os membros e os tipos do assembly System.Data.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
|Tipo ou membro|Valor(es) de HPA|  
|--------------------|--------------------|  
|System.Data.SqlClient.SqlCommand.BeginExecuteNonQuery ()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteReader()|ExternalThreading|  
|System.Data.SqlClient.SqlCommand.BeginExecuteXmlReader()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency..ctor ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Start ()|ExternalThreading|  
|System.Data.SqlClient.SqlDependency.Stop()|ExternalThreading|  
|System.Data.TypedDataSetGenerator|SharedState, Sincronização|  
|System.Xml.XmlDataDocument|Synchronization|  
  
## <a name="see-also"></a>Consulte Também  
 [Atributos de proteção do host e programação de integração CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos e membros não permitidos em Microsoft. VisualBasic. dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos e membros não permitidos em mscorlib. dll](disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos e membros não permitidos em System. dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros desaprovados no System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
