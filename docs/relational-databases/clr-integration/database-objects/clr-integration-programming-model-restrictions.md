---
title: Restrições do modelo de programação de integração da CLR | Microsoft Docs
description: O SQL Server realiza verificações de código em objetos de banco de dados gerenciados quando eles são registrados pela primeira vez usando CREATE ASSEMBLY e em tempo de execução.
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
ms.openlocfilehash: 83b73909cf1844796640a83910ee609eadd7dba4
ms.sourcegitcommit: b2cc3f213042813af803ced37901c5c9d8016c24
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2020
ms.locfileid: "81488507"
---
# <a name="clr-integration-programming-model-restrictions"></a>Restrições do modelo de programação da Integração CLR
[!INCLUDE[appliesto-ss-asdbmi-xxxx-xxx-md](../../../includes/appliesto-ss-asdbmi-xxxx-xxx-md.md)]
  Quando você está construindo um procedimento armazenado gerenciado ou outro objeto de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados gerenciado, existem certas verificações de código realizadas por essa necessidade de ser considerada. [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]realiza verificações no conjunto de código gerenciado quando ele é registrado pela primeira vez no banco de dados, usando a declaração **CREATE ASSEMBLY** e também em tempo de execução. O código gerenciado também é verificado em runtime porque, em um assembly, talvez haja caminhos de código que jamais possam ser alcançados em runtime.  Isso proporciona flexibilidade para registrar, especialmente, assemblies de terceiros, logo um assembly não seria bloqueado quando houvesse um código 'não seguro' projetado para execução em um ambiente do cliente, mas que jamais seria executado no CLR hospedado. Os requisitos que o código gerenciado deve atender dependem se o conjunto está registrado como **SAFE**, **EXTERNAL_ACCESS**ou **UNSAFE**, **SAFE** sendo o mais rigoroso, e estão listados abaixo.  
  
 Além das restrições colocadas nos assemblies de código gerenciado, também há permissões de segurança de código que são concedidas. O CLR (Common Language Runtime) oferece suporte a um modelo de segurança chamado segurança de acesso do código (CAS) destinado ao código gerenciado. Nesse modelo, são concedidas permissões a assemblies com base na identidade do código. Os conjuntos **SAFE,** **EXTERNAL_ACCESS**e **UNSAFE** têm diferentes permissões CAS. Para obter mais informações, consulte [CLR Integration Code Access Security](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md).  
  
## <a name="create-assembly-checks"></a>Verificações de CREATE ASSEMBLY  
 Quando a declaração **CREATE ASSEMBLY** é executada, as seguintes verificações são executadas para cada nível de segurança.  Se alguma verificação falhar, **o CREATE ASSEMBLY** falhará com uma mensagem de erro.  
  
### <a name="global-any-security-level"></a>Global (qualquer nível de segurança)  
 Todos os assemblies referenciados devem atender a um ou mais dos seguintes critérios:  
  
-   O assembly já está registrado no banco de dados.  
  
-   O assembly é um daqueles para os quais há suporte. Para obter mais informações, consulte [Bibliotecas-quadro .NET suportadas](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md). NET .  
  
-   Você está usando **CREATE ASSEMBLY FROM**_\<location>,_ e todos os conjuntos referenciados e suas dependências estão disponíveis no * \<local>*.  
  
-   Você está usando **CREATE ASSEMBLY FROM**_\<bytes ...>,_ e todas as referências são especificadas através de bytes separados por espaço.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todas as assembleias **EXTERNAL_ACCESS** devem atender aos seguintes critérios:  
  
-   Não são usados campos estáticos para armazenar informações. São permitidos campos estáticos somente leitura.  
  
-   O teste PEVerify passou. A ferramenta PEVerify (peverify.exe), que verifica se o código MSIL e os metadados associados atendem aos requisitos de segurança do tipo, é fornecida com o SDK do .NET Framework.  
  
-   A sincronização, por exemplo, com a classe **SynchronizationAttribute,** não é usada.  
  
-   Não são usados métodos Finalizer.  
  
 Os seguintes atributos personalizados são proibidos em **EXTERNAL_ACCESS** assembléias:  
  
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
  
-   Todas as **condições EXTERNAL_ACCESS** de montagem são verificadas.  
  
## <a name="runtime-checks"></a>Verificações de runtime  
 Em runtime, o assembly do código é verificado em relação às seguintes condições. Se alguma dessas condições for encontrada, o código gerenciado não terá permissão de execução, e uma exceção será lançada.  
  
### <a name="unsafe"></a>UNSAFE  
 Carregar um conjunto- explicitamente chamando o método **System.Reflection.Assembly.Load()** de uma matriz de bytes, ou implicitamente através do uso do **namespace Reflection.Emit-é** permitido.  
  
### <a name="external_access"></a>EXTERNAL_ACCESS  
 Todas **as condições inseguras** são verificadas.  
  
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
  
 Para obter mais informações sobre HPAs e uma lista de tipos e membros proibidos nas assembléias suportadas, consulte [Host Protection Attributes e CLR Integration Programming](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md).  
  
### <a name="safe"></a>SAFE  
 Todos os **EXTERNAL_ACCESS** condições são verificados.  
  
## <a name="see-also"></a>Consulte Também  
 [Bibliotecas-quadro .NET suportadas](../../../relational-databases/clr-integration/database-objects/supported-net-framework-libraries.md)   
 [Segurança de acesso ao código de integração clr](../../../relational-databases/clr-integration/security/clr-integration-code-access-security.md)   
 [Atributos de proteção de host e programação de integração CLR](../../../relational-databases/clr-integration-security-host-protection-attributes/host-protection-attributes-and-clr-integration-programming.md)   
 [Criando um assembly](../../../relational-databases/clr-integration/assemblies/creating-an-assembly.md)  
  
  
