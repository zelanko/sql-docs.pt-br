---
title: Restrições do modelo de programação de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 03/17/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: clr
ms.topic: reference
helpviewer_keywords:
- common language runtime [SQL Server], programming model restrictions
- assemblies [CLR integration], CREATE ASSEMBLY checks
- programming model restrictions [CLR integration]
- assemblies [CLR integration], runtime checks
ms.assetid: 2446afc2-9d21-42d3-9847-7733d3074de9
author: rothja
ms.author: jroth
ms.openlocfilehash: c019b50f896109a699869d748d8eef20b57d6edb
ms.sourcegitcommit: 734529a6f108e6ee6bfce939d8be562d405e1832
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/02/2019
ms.locfileid: "70212368"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrições do modelo de programação da Integração CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Quando você está criando um procedimento armazenado gerenciado ou outro objeto de banco de dados gerenciado, há determinadas verificações de código executadas por [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que precisam ser consideradas. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] executa verificações no assembly de código gerenciado quando ele é registrado pela primeira vez no banco de dados, usando a instrução **Create assembly** e também em tempo de execução. O código gerenciado também é verificado em runtime porque, em um assembly, talvez haja caminhos de código que jamais possam ser alcançados em runtime.  Isso proporciona flexibilidade para registrar, especialmente, assemblies de terceiros, logo um assembly não seria bloqueado quando houvesse um código 'não seguro' projetado para execução em um ambiente do cliente, mas que jamais seria executado no CLR hospedado. Os requisitos que o código gerenciado deve atender dependem de se o assembly está registrado como **seguro**, **EXTERNAL_ACCESS** **ou não seguro,** **seguro** sendo o mais estrito e está listado abaixo.  
  
 Além das restrições colocadas nos assemblies de código gerenciado, também há permissões de segurança de código que são concedidas. O CLR (Common Language Runtime) oferece suporte a um modelo de segurança chamado segurança de acesso do código (CAS) destinado ao código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Os assemblies **seguros**, **EXTERNAL_ACCESS**e não **seguros** têm permissões de CAS diferentes. Para obter mais informações, consulte [segurança de acesso ao código de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Verificações de CREATE ASSEMBLY  
 Quando a instrução **Create assembly** é executada, as verificações a seguir são executadas para cada nível de segurança.  Se qualquer verificação falhar, **Create assembly** falhará com uma mensagem de erro.  
  
### <a name="global-any-security-level"></a>Global (qualquer nível de segurança)  
 Todos os assemblies referenciados devem atender a um ou mais dos seguintes critérios:  
  
-   O assembly já está registrado no banco de dados.  
  
-   O assembly é um daqueles para os quais há suporte. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md).  
  
-   Você está usando **criar assembly do** _\<local >_ e todos os assemblies referenciados e suas dependências estão disponíveis no *> local\<* .  
  
-   Você está usando **criar assembly de** _\<bytes... >_ e todas as referências são especificadas por meio de bytes separados por espaço.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todos os assemblies de **EXTERNAL_ACCESS** devem atender aos seguintes critérios:  
  
-   Não são usados campos estáticos para armazenar informações. São permitidos campos estáticos somente leitura.  
  
-   O teste PEVerify passou. A ferramenta PEVerify (peverify.exe), que verifica se o código MSIL e os metadados associados atendem aos requisitos de segurança do tipo, é fornecida com o SDK do .NET Framework.  
  
-   A sincronização, por exemplo, com a classe **SynchronizationAttribute** , não é usada.  
  
-   Não são usados métodos Finalizer.  
  
 Os seguintes atributos personalizados não são permitidos em assemblies de **EXTERNAL_ACCESS** :  
  
-   System.ContextStaticAttribute  
  
-   System.MTAThreadAttribute  
  
-   System.Runtime.CompilerServices.MethodImplAttribute  
  
-   System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
  
-   System.Runtime.Remoting.Contexts.ContextAttribute  
  
-   System.Runtime.Remoting.Contexts.SynchronizationAttribute  
  
-   System.Runtime.InteropServices.DllImportAttribute  
  
-   System.Security.Permissions.CodeAccessSecurityAttribute  
  
-   System.Security.SuppressUnmanagedCodeSecurityAttribute  
  
-   System.Security.UnverifiableCodeAttribute  
  
-   System.STAThreadAttribute  
  
-   System.ThreadStaticAttribute  
  
### <a name="safe"></a>SAFE  
  
-   Todas as condições de assembly **EXTERNAL_ACCESS** são verificadas.  
  
## <a name="runtime-checks"></a>Verificações de runtime  
 Em runtime, o assembly do código é verificado em relação às seguintes condições. Se alguma dessas condições for encontrada, o código gerenciado não terá permissão de execução, e uma exceção será lançada.  
  
### <a name="unsafe"></a>UNSAFE  
 Carregar um assembly-seja explicitamente chamando o método **System. Reflection. assembly. Load ()** de uma matriz de bytes ou implicitamente pelo uso do namespace **Reflection. Emit** -não é permitido.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todas as condições **não seguras** são verificadas.  
  
 São desaprovados todos os tipos e métodos anotados com os seguintes valores HPA (atributo de proteção de host) na lista de assemblies para a qual há suporte.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Synchronization  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Para obter mais informações sobre HPAs e uma lista de tipos não permitidos e membros nos assemblies com suporte, consulte [atributos de proteção do host e programação de integração do CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Todas as condições de **EXTERNAL_ACCESS** são verificadas.  
  
## <a name="see-also"></a>Consulte também  
 [Bibliotecas de .NET Framework com suporte](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
   de [segurança de acesso a código de integração CLR](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)  
 [Atributos de proteção do host e programação de integração do CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
