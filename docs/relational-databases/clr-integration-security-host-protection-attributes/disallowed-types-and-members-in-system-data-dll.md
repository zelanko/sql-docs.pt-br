---
title: "Não permitido tipos e membros de System.Data.dll | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- common language runtime [SQL Server], host protection attributes
ms.assetid: ee5f55e9-fbef-401a-be18-a2e5873c8720
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: d9a560a3dc5db0d6c13b5b77e0b0f4c707a4e43a
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="disallowed-types-and-members-in-systemdatadll"></a>Tipos e membros não permitidos em System.Data.dll
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] programação integration (CLR) proíbe o uso de um tipo ou membro que tem um **HostProtectionAttribute** que especifica um **System.Security.Permissions.HostProtectionResource**  enumeração com um valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**,  **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**,  **Sincronização**, ou **UI**. A tabela a seguir lista os membros e os tipos do assembly System.Data.dll cujos valores de HPA (atributo de proteção de host) não são permitidos.  
  
> [!NOTE]  
>  Esta lista foi gerada dos assembly com suporte. Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
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
 [Atributos de proteção de host e programação da integração CLR](../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Tipos desaprovados e membros em Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)   
 [Tipos desaprovados e membros de mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)   
 [Tipos desaprovados e membros desabilitados em System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)   
 [Tipos e membros não permitidos no System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
  
  
