---
title: Atributos de proteção do host (CLR) do Common Language Runtime (CLR)
description: O CLR fornece um mecanismo para anotar APIs gerenciadas no Framework .NET com atributos como SharedState, Synchronization e ExternalProcessMgmt.
ms.custom: seo-lt-2019
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
author: rothja
ms.author: jroth
ms.openlocfilehash: 2aeaeb5d4eb06d6d632a59300225d01cc4376369
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488040"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de proteção de host e programação da Integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O CLR (Common Language Runtime) fornece um mecanismo para anotar APIs (interfaces de programação de aplicativo ) gerenciadas que fazem parte do .NET Framework com determinados atributos que podem ser de interesse de um host do CLR como, por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Entre os exemplos desses HPAs (atributos de proteção de host) estão:  
  
-   **Estado compartilhado**, que indica se a API expõe a capacidade de criar ou gerenciar o estado compartilhado (por exemplo, campos de classe estática).  
  
-   **Sincronização**, que indica se a API expõe a capacidade de executar a sincronização entre os segmentos.  
  
-   **ExternalProcessMgmt**, que indica se a API expõe uma maneira de controlar o processo de host.  
  
 Dados esses atributos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica uma lista de HPAs desaprovadas no ambiente hospedado por meio da CAS (segurança de acesso do código). Os requisitos cas são especificados por um dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] três conjuntos de permissões: **SAFE**, **EXTERNAL_ACCESS**ou **UNSAFE**. Um desses três níveis de segurança é especificado quando o conjunto é registrado no servidor, usando a declaração **CREATE ASSEMBLY.** A execução de códigos dentro dos conjuntos **de** permissões SAFE ou **EXTERNAL_ACCESS** deve evitar certos tipos ou membros que tenham o atributo **System.Security.Permissions.HostProtectionAttribute** aplicado. Para obter mais informações, consulte Criando um Modelo de [Programação de Integração de](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md) [Montagem](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) e CLR .  
  
 O **HostProtectionAttribute** não é uma permissão de segurança, mas uma maneira de melhorar a confiabilidade, na medida em que identifica construtos de código específicos, tipos ou métodos, que o host pode proibir. O uso do **HostProtectionAttribute** impõe um modelo de programação que ajuda a proteger a estabilidade do host.  
  
## <a name="host-protection-attributes"></a>Atributos de proteção de host  
 HPAs identificam tipos ou membros que não se ajustam ao modelo de programação de host e representam os seguintes níveis crescentes de ameaça à confiabilidade:  
  
-   Do contrário, benignos.  
  
-   Poderia levar à desestabilização do código de usuário gerenciado por servidor.  
  
-   Poderia levar à desestabilização do próprio processo do servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]proíbe o uso de um tipo ou membro que tenha um **HostProtectionAttribute** que especifica um **System.Security.Permissions.HostProtectionEnumeração** de recursos com um valor de **ExternalProcessMgmt,** **ExternalThreading,** **MayLeakOnAbort,** **SecurityInfrastructure,** **SelfAffectingProcessMgmnt,** **SelfAffectingThreading,** **SharedState,** **Synchronization**ou **UI**. Isso impede que os assemblies chamem membros que permitam compartilhar o estado, realizar a sincronização, causar um vazamento de recurso na terminação ou afetar a integridade do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos e membros desaprovados  
 Os tópicos a seguir identificam tipos e membros [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]cujos valores **hostProtectionResource** são proibidos por .  
  
> [!NOTE]  
>  As listas deste tópico foram geradas dos assembly com suporte.  Para obter mais informações, consulte [Bibliotecas-quadro .NET suportadas](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md). NET .  
  
## <a name="in-this-section"></a>Nesta seção  
 [Tipos desaprovados e membros em Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Lista os tipos e os membros de Microsoft.VisualBasic.dll cujos valores HPA não são permitidos.  
  
 [Membros e tipos não permitidos em mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Lista os tipos e os membros de mscorlib.dll cujos valores HPA são desaprovados.  
  
 [Disallowed Types and Members In System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Lista os tipos e os membros de System.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Lista os tipos e os membros de System.Data.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros desaprovados no System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Lista os tipos e os membros de System.Core.dll cujos valores HPA são desaprovados.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de acesso ao código de integração clr](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação de integração do CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Criando um assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
