---
title: Restrições do modelo de programação de integração CLR | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 5b9385d9b801ee615a377a78a44e087589a581ac
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84953469"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrições do modelo de programação da Integração CLR
  Quando você está criando um procedimento armazenado gerenciado ou outro objeto de banco de dados gerenciado, há determinadas verificações de código executadas pelo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] realiza verificações no assembly de código gerenciado quando ele é registrado pela primeira vez no banco de dados, usando a `CREATE ASSEMBLY` instrução e também em tempo de execução. O código gerenciado também é verificado em runtime porque, em um assembly, talvez haja caminhos de código que jamais possam ser alcançados em runtime.  Isso proporciona flexibilidade para registrar, especialmente, assemblies de terceiros, logo um assembly não seria bloqueado quando houvesse um código 'não seguro' projetado para execução em um ambiente do cliente, mas que jamais seria executado no CLR hospedado. Os requisitos que o código gerenciado deve atender dependem se o assembly está registrado como `SAFE` , `EXTERNAL_ACCESS` ou `UNSAFE` , `SAFE` sendo o mais estrito, e está listado abaixo.  
  
 Além das restrições colocadas nos assemblies de código gerenciado, também há permissões de segurança de código que são concedidas. O CLR (Common Language Runtime) oferece suporte a um modelo de segurança chamado segurança de acesso do código (CAS) destinado ao código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Os assemblies `SAFE`, `EXTERNAL_ACCESS` e `UNSAFE` têm permissões CAS diferentes. Para obter mais informações, consulte [segurança de acesso ao código de integração CLR](../security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Verificações de CREATE ASSEMBLY  
 Quando a instrução `CREATE ASSEMBLY` é executada, as seguintes verificações são executadas em cada nível de segurança.  Se houver falha em alguma verificação, `CREATE ASSEMBLY` apresentará uma mensagem de erro.  
  
### <a name="global-any-security-level"></a>Global (qualquer nível de segurança)  
 Todos os assemblies referenciados devem atender a um ou mais dos seguintes critérios:  
  
-   O assembly já está registrado no banco de dados.  
  
-   O assembly é um daqueles para os quais há suporte. Para obter mais informações, consulte [bibliotecas de .NET Framework com suporte](supported-net-framework-libraries.md).  
  
-   Você está usando `CREATE ASSEMBLY FROM` o * \<location> ,* e todos os assemblies referenciados e suas dependências estão disponíveis no *\<location>* .  
  
-   Você está usando `CREATE ASSEMBLY FROM` * \<bytes ...> ,* e todas as referências são especificadas por meio de bytes separados por espaço.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todos os assemblies `EXTERNAL_ACCESS` devem atender aos seguintes critérios:  
  
-   Não são usados campos estáticos para armazenar informações. São permitidos campos estáticos somente leitura.  
  
-   O teste PEVerify passou. A ferramenta PEVerify (peverify.exe), que verifica se o código MSIL e os metadados associados atendem aos requisitos de segurança do tipo, é fornecida com o SDK do .NET Framework.  
  
-   A sincronização, por exemplo com a classe `SynchronizationAttribute`, não é usada.  
  
-   Não são usados métodos Finalizer.  
  
 Os seguintes atributos personalizados são desaprovados no assembly `EXTERNAL_ACCESS`:  
  
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
  
-   Todas as condições do assembly `EXTERNAL_ACCESS` são verificadas.  
  
## <a name="runtime-checks"></a>Verificações de runtime  
 Em runtime, o assembly do código é verificado em relação às seguintes condições. Se alguma dessas condições for encontrada, o código gerenciado não terá permissão de execução, e uma exceção será lançada.  
  
### <a name="unsafe"></a>UNSAFE  
 Carregar um assembly-seja explicitamente chamando o `System.Reflection.Assembly.Load()` método de uma matriz de bytes ou implicitamente através do uso de `Reflection.Emit` namespace-não é permitido.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todas as condições `UNSAFE` são verificadas.  
  
 São desaprovados todos os tipos e métodos anotados com os seguintes valores HPA (atributo de proteção de host) na lista de assemblies para a qual há suporte.  
  
-   SelfAffectingProcessMgmt  
  
-   SelfAffectingThreading  
  
-   Sincronização  
  
-   SharedState  
  
-   ExternalProcessMgmt  
  
-   ExternalThreading  
  
-   SecurityInfrastructure  
  
-   MayLeakOnAbort  
  
-   UI  
  
 Para obter mais informações sobre HPAs e uma lista de tipos não permitidos e membros nos assemblies com suporte, consulte [atributos de proteção do host e programação de integração do CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Todas as condições `EXTERNAL_ACCESS` são verificadas.  
  
## <a name="see-also"></a>Consulte Também  
 [Bibliotecas de .NET Framework com suporte](supported-net-framework-libraries.md)   
 [Segurança de acesso ao código de integração CLR](../security/clr-integration-code-access-security.md)   
 [Atributos de proteção do host e programação de integração CLR](../../clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Criando um assembly](../assemblies/creating-an-assembly.md)  
  
  
