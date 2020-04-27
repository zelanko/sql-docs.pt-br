---
title: Atributos de proteção do host e programação de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: 68f1f114002ab0ef38c7565a523723a06958048d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "62874351"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de proteção de host e programação da Integração CLR
  O CLR (Common Language Runtime) fornece um mecanismo para anotar APIs (interfaces de programação de aplicativo ) gerenciadas que fazem parte do .NET Framework com determinados atributos que podem ser de interesse de um host do CLR como, por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Entre os exemplos desses HPAs (atributos de proteção de host) estão:  
  
-   `SharedState`, que indica se a API expõe a capacidade de criar ou gerenciar estado compartilhado (por exemplo, campos de classe estáticos).  
  
-   `Synchronization`, que indica se a API expõe a capacidade para executar sincronização entre threads.  
  
-   `ExternalProcessMgmt`, que indica se a API expõe um modo de controlar o processo de host.  
  
 Dados esses atributos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica uma lista de HPAs desaprovadas no ambiente hospedado por meio da CAS (segurança de acesso do código). Os requisitos de CAs são especificados por um dos três conjuntos de permissões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]: `SAFE`, `EXTERNAL_ACCESS` ou `UNSAFE`. Um desses três níveis de segurança é especificado quando o assembly é registrado no servidor, usando a instrução `CREATE ASSEMBLY`. Código em execução nos conjuntos de permissões `SAFE` ou `EXTERNAL_ACCESS` deve evitar determinados tipos ou membros que tenham o atributo `System.Security.Permissions.HostProtectionAttribute` aplicado. Para obter mais informações, consulte [criando um assembly](../clr-integration/assemblies/creating-an-assembly.md) e [restrições de modelo de programação de integração CLR](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 `HostProtectionAttribute` não é uma permissão de segurança tanto quanto uma forma de aumentar a confiabilidade; ela identifica construções de código específicas, tipos ou métodos, que o host pode desautorizar. O uso do `HostProtectionAttribute` impõe um modelo de programação que ajuda a proteger a estabilidade do host.  
  
## <a name="host-protection-attributes"></a>Atributos de proteção de host  
 HPAs identificam tipos ou membros que não se ajustam ao modelo de programação de host e representam os seguintes níveis crescentes de ameaça à confiabilidade:  
  
-   Do contrário, benignos.  
  
-   Poderia levar à desestabilização do código de usuário gerenciado por servidor.  
  
-   Poderia levar à desestabilização do próprio processo do servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Não permite `HostProtectionAttribute` o uso de um tipo ou membro que tenha um que especifique uma `System.Security.Permissions.HostProtectionResource` enumeração com um valor de `ExternalProcessMgmt`, `ExternalThreading`, `MayLeakOnAbort` `SecurityInfrastructure` `SelfAffectingProcessMgmnt` `SelfAffectingThreading`,,,, `SharedState`, `Synchronization`ou. `UI` Isso impede que os assemblies chamem membros que permitam compartilhar o estado, realizar a sincronização, causar um vazamento de recurso na terminação ou afetar a integridade do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos e membros desaprovados  
 Os seguintes tópicos identificam tipos e membros cujos valores `HostProtectionResource` são desaprovados por [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  As listas deste tópico foram geradas dos assembly com suporte.  Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Tipos desaprovados e membros em Microsoft.VisualBasic.dll](disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Lista os tipos e os membros de Microsoft.VisualBasic.dll cujos valores HPA não são permitidos.  
  
 [Membros e tipos não permitidos em mscorlib.dll](disallowed-types-and-members-in-mscorlib-dll.md)  
 Lista os tipos e os membros de mscorlib.dll cujos valores HPA são desaprovados.  
  
 [Disallowed Types and Members In System.dll](disallowed-types-and-members-in-system-dll.md)  
 Lista os tipos e os membros de System.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System.Data.dll](disallowed-types-and-members-in-system-data-dll.md)  
 Lista os tipos e os membros de System.Data.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros desaprovados no System.Core.dll](disallowed-types-and-members-in-system-core-dll.md)  
 Lista os tipos e os membros de System.Core.dll cujos valores HPA são desaprovados.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de acesso ao código de integração CLR](../clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação de integração CLR](../clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Criando um assembly](../clr-integration/assemblies/creating-an-assembly.md)  
  
  
