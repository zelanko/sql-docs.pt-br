---
title: Hospedar os atributos de proteção e programação da integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.suite: sql
ms.technology: clr
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- host protection attributes [CLR integration]
- HostProtectionAttribute [CLR integration]
- common language runtime [SQL Server], host protection attributes
- disallowed types and members [CLR integration]
- common language runtime [SQL Server], disallowed types and members
- HPAs [CLR integration]
ms.assetid: 268078df-63ca-4c03-a8e7-7108bcea9697
caps.latest.revision: 28
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 501c85065f0519987a7837042bec45b5d5b4db9d
ms.sourcegitcommit: 022d67cfbc4fdadaa65b499aa7a6a8a942bc502d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37350308"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de proteção de host e programação da Integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O CLR (Common Language Runtime) fornece um mecanismo para anotar APIs (interfaces de programação de aplicativo ) gerenciadas que fazem parte do .NET Framework com determinados atributos que podem ser de interesse de um host do CLR como, por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Entre os exemplos desses HPAs (atributos de proteção de host) estão:  
  
-   **SharedState**, que indica se a API expõe a capacidade de criar ou gerenciar o estado (por exemplo, campos de classe estáticos) compartilhado.  
  
-   **Sincronização**, que indica se a API expõe a capacidade de realizar a sincronização entre threads.  
  
-   **ExternalProcessMgmt**, que indica se a API expõe uma maneira de controlar o processo de host.  
  
 Dados esses atributos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica uma lista de HPAs desaprovadas no ambiente hospedado por meio da CAS (segurança de acesso do código). Os requisitos de CAS são especificados por um dos três [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de permissões: **seguro**, **EXTERNAL_ACCESS**, ou **UNSAFE**. Um desses três níveis de segurança é especificado quando o assembly é registrado no servidor, usando o **CREATE ASSEMBLY** instrução. Código em execução dentro de **seguro** ou **EXTERNAL_ACCESS** conjuntos de permissões devem evitar determinados tipos ou membros que têm o **System.Security.Permissions.HostProtectionAttribute** atributo aplicado. Para obter mais informações, consulte [criando um Assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) e [restrições do modelo de programação de integração de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 O **HostProtectionAttribute** não é uma permissão de segurança tanto quanto constrói uma maneira de aumentar a confiabilidade, ela identifica o código específico, tipos ou métodos, que o host pode desautorizar. O uso do **HostProtectionAttribute** impõe um modelo de programação que ajuda a proteger a estabilidade do host.  
  
## <a name="host-protection-attributes"></a>Atributos de proteção de host  
 HPAs identificam tipos ou membros que não se ajustam ao modelo de programação de host e representam os seguintes níveis crescentes de ameaça à confiabilidade:  
  
-   Do contrário, benignos.  
  
-   Poderia levar à desestabilização do código de usuário gerenciado por servidor.  
  
-   Poderia levar à desestabilização do próprio processo do servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não permite o uso de um tipo ou membro que tem um **HostProtectionAttribute** que especifica um **System.Security.Permissions.HostProtectionResource** enumeração com um valor de ** ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, ** SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **sincronização**, ou **deinterfacedousuário**. Isso impede que os assemblies chamem membros que permitam compartilhar o estado, realizar a sincronização, causar um vazamento de recurso na terminação ou afetar a integridade do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos e membros desaprovados  
 Os seguintes tópicos identificam tipos e membros cujos **HostProtectionResource** valores não são permitidos pela [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  As listas deste tópico foram geradas dos assembly com suporte.  Para obter mais informações, consulte [suporte para bibliotecas do .NET Framework](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Tipos e membros não permitidos em Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Lista os tipos e os membros de Microsoft.VisualBasic.dll cujos valores HPA não são permitidos.  
  
 [Tipos e membros não permitidos em mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Lista os tipos e os membros de mscorlib.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Lista os tipos e os membros de System.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Lista os tipos e os membros de System.Data.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos no System.Core.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Lista os tipos e os membros de System.Core.dll cujos valores HPA são desaprovados.  
  
## <a name="see-also"></a>Consulte também  
 [Segurança de acesso do código de integração de CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação de integração de CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Criando um assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
