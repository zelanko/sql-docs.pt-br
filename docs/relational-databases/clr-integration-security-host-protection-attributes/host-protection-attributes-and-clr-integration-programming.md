---
title: Atributos de proteção do host do CLR (Common Language Runtime)
description: O Common Language Runtime (CLR) fornece um mecanismo para anotar as APIs (interfaces de programação de aplicativo) gerenciadas que fazem parte do .NET Framework com determinados atributos.
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
ms.openlocfilehash: 733e4adc69570dd98e6e0ad5448820607ade6329
ms.sourcegitcommit: 792c7548e9a07b5cd166e0007d06f64241a161f8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/19/2019
ms.locfileid: "75258751"
---
# <a name="host-protection-attributes-and-clr-integration-programming"></a>Atributos de proteção de host e programação da Integração CLR
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  O CLR (Common Language Runtime) fornece um mecanismo para anotar APIs (interfaces de programação de aplicativo ) gerenciadas que fazem parte do .NET Framework com determinados atributos que podem ser de interesse de um host do CLR como, por exemplo, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], desde o [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)]. Entre os exemplos desses HPAs (atributos de proteção de host) estão:  
  
-   **SharedState**, que indica se a API expõe a capacidade de criar ou gerenciar o estado compartilhado (por exemplo, campos de classe estática).  
  
-   **Sincronização**, que indica se a API expõe a capacidade de executar a sincronização entre threads.  
  
-   **ExternalProcessMgmt**, que indica se a API expõe uma maneira de controlar o processo do host.  
  
 Dados esses atributos, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] especifica uma lista de HPAs desaprovadas no ambiente hospedado por meio da CAS (segurança de acesso do código). Os requisitos de CAS são especificados por um dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] três conjuntos de permissões: **seguro**, **EXTERNAL_ACCESS**ou **não seguro**. Um desses três níveis de segurança é especificado quando o assembly é registrado no servidor, usando a instrução **Create assembly** . O código em execução nos conjuntos de permissões **seguro** ou **EXTERNAL_ACCESS** deve evitar certos tipos ou membros que tenham o atributo **System. Security. Permissions. HostProtectionAttribute** aplicado. Para obter mais informações, consulte [criando um assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md) e [restrições de modelo de programação de integração CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md).  
  
 O **HostProtectionAttribute** não é uma permissão de segurança como uma maneira de melhorar a confiabilidade, pois identifica construções de código específicas, tipos ou métodos, que o host pode não permitir. O uso do **HostProtectionAttribute** impõe um modelo de programação que ajuda a proteger a estabilidade do host.  
  
## <a name="host-protection-attributes"></a>Atributos de proteção de host  
 HPAs identificam tipos ou membros que não se ajustam ao modelo de programação de host e representam os seguintes níveis crescentes de ameaça à confiabilidade:  
  
-   Do contrário, benignos.  
  
-   Poderia levar à desestabilização do código de usuário gerenciado por servidor.  
  
-   Poderia levar à desestabilização do próprio processo do servidor.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]Não permite o uso de um tipo ou membro que tenha um **HostProtectionAttribute** que especifique uma enumeração **System. Security. Permissions. HostProtectionResource** com um valor de **ExternalProcessMgmt**, **ExternalThreading**, **MayLeakOnAbort**, **SecurityInfrastructure**, **SelfAffectingProcessMgmnt**, **SelfAffectingThreading**, **SharedState**, **Synchronization**ou **UI**. Isso impede que os assemblies chamem membros que permitam compartilhar o estado, realizar a sincronização, causar um vazamento de recurso na terminação ou afetar a integridade do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
### <a name="disallowed-types-and-members"></a>Tipos e membros desaprovados  
 Os tópicos a seguir identificam tipos e membros cujos valores de **HostProtectionResource** não são [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]permitidos pelo.  
  
> [!NOTE]  
>  As listas deste tópico foram geradas dos assembly com suporte.  Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
## <a name="in-this-section"></a>Nesta seção  
 [Tipos desaprovados e membros em Microsoft.VisualBasic.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-microsoft-visualbasic-dll.md)  
 Lista os tipos e os membros de Microsoft.VisualBasic.dll cujos valores HPA não são permitidos.  
  
 [Membros e tipos não permitidos em mscorlib.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-mscorlib-dll.md)  
 Lista os tipos e os membros de mscorlib.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System. dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-dll.md)  
 Lista os tipos e os membros de System.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System.Data.dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-data-dll.md)  
 Lista os tipos e os membros de System.Data.dll cujos valores HPA são desaprovados.  
  
 [Tipos e membros não permitidos em System. Core. dll](../../relational-databases/clr-integration-security-host-protection-attributes/disallowed-types-and-members-in-system-core-dll.md)  
 Lista os tipos e os membros de System.Core.dll cujos valores HPA são desaprovados.  
  
## <a name="see-also"></a>Consulte Também  
 [Segurança de acesso ao código de integração CLR](../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Restrições do modelo de programação de integração CLR](../../relational-databases/clr-integration/database-objects/clr-integration-programming-model-restrictions.md)   
 [Criando um assembly](../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
