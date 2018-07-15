---
title: Não permitido de tipos e membros no DLL | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
caps.latest.revision: 17
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 728de68145c4deb7b259c7b59687e29e960c822a
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37353968"
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos e membros não permitidos em System.Data.dll
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programação de integração (CLR) de linguagem comum não permite o uso de um tipo ou membro que tem um `HostProtectionAttribute` que especifica um `System.Security.Permissions.HostProtectionResource` enumeração com um valor de `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort`, `SecurityInfrastructure`, `SelfAffectingProcessMgmnt`, `SelfAffectingThreading`, **SharedState**, `Synchronization`, ou `UI`. A tabela a seguir lista os membros e os tipos do assembly System.Data.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Atributos de proteção de host e programação da integração CLR](host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos desaprovados e membros no VisualBasic](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos desaprovados e membros em mscorlib. dll](disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos desaprovados e membros em System. dll](disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros não permitidos no System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
  
  
