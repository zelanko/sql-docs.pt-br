---
title: Criando Assemblies | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: clr
ms.reviewer: 
ms.suite: sql
ms.technology: docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- designing assemblies [SQL Server]
- assemblies [CLR integration], designing
ms.assetid: 9c07f706-6508-41aa-a4d7-56ce354f9061
caps.latest.revision: "29"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: ce4e2e7fb36146d9e7e84a8a5c0a1b2f3fe09f58
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="assemblies---designing"></a>Assemblies - criação
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]Este tópico descreve os seguintes fatores que você deve considerar ao projetar assemblies:  
  
-   Empacotando assemblies  
  
-   Gerenciando a segurança do assembly  
  
-   Restrições em assemblies  
  
## <a name="packaging-assemblies"></a>Empacotando assemblies  
 Um assembly pode conter funcionalidade para mais de uma rotina do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou tipo em suas classes e métodos. A maior parte do tempo, faz sentido empacotar a funcionalidade de rotinas que executam funções relacionadas dentro do mesmo assembly, especialmente se essas rotinas compartilharem classes cujos métodos chamam um ao outro. Por exemplo, classes que executam tarefas de gerenciamento de entrada de dados para gatilhos CLR (Common Language Runtime) e procedimentos armazenados CLR podem ser empacotados no mesmo assembly. Isso porque os métodos para essas classes têm maior probabilidade de chamar um ao outro do que aqueles de tarefas menos relacionadas.  
  
 Quando você estiver empacotando código em um assembly, você deverá considerar o seguinte:  
  
-   Tipos de dados CLR definidos pelo usuário e índices que dependem de funções CLR definidas pelo usuário podem fazer com que dados persistentes fiquem no banco de dados que dependem do assembly. Modificar o código de um assembly é frequentemente mais complexo quando há dados persistentes que dependem do assembly no banco de dados. Portanto, geralmente é melhor separar o código onde haja dependências de dados persistentes (como tipos definidos pelo usuário e índices com funções definidas pelo usuário) do código que não tenha tal dependência de dados persistentes. Para obter mais informações, consulte [implementando Assemblies](../../relational-databases/clr-integration/assemblies-implementing.md) e [ALTER ASSEMBLY &#40; Transact-SQL &#41; ](../../t-sql/statements/alter-assembly-transact-sql.md).  
  
-   Se uma parte do código gerenciado requerer permissão mais alta, será melhor separar aquele código em um assembly separado do código que não requer tal permissão.  
  
## <a name="managing-assembly-security"></a>Gerenciando segurança de assembly  
 Você pode controlar quanto um assembly pode acessar recursos protegidos por Código de .NET Access Security quando executar código gerenciado. Você faz isto especificando um de três conjuntos de permissão quando você cria ou modifica um assembly: SAFE, EXTERNAL_ACCESS ou UNSAFE.  
  
### <a name="safe"></a>SAFE  
 SAFE é o conjunto de permissões padrão e é o mais restritivo. Código executado por um assembly com permissões SAFE não pode acessar recursos do sistema externo, como arquivos, rede, variáveis de ambiente ou Registro. O código SAFE pode acessar dados dos bancos de dados locais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou pode executar computações e lógica empresarial que não envolvam acesso de recursos fora dos bancos de dados locais.  
  
 A maioria dos assemblies executa tarefas de computação e gerenciamento de dados sem ter de acessar recursos fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Portanto, nós recomendamos SAFE como conjunto de permissões de assembly.  
  
### <a name="externalaccess"></a>EXTERNAL_ACCESS  
 EXTERNAL_ACCESS permite que assemblies acessem certos recursos do sistema externo como arquivos, redes, serviços da Web, variáveis ambientais e Registro. Somente logons do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com permissões EXTERNAL ACCESS podem criar assemblies EXTERNAL_ACCESS.  
  
 Assemblies SAFE e EXTERNAL_ACCESS só podem conter código do tipo seguro verificável. Isso significa que esses assemblies só podem acessar classes por pontos bem definido de entrada que sejam válidos para a definição de tipo. Portanto, eles não podem acessar arbitrariamente buffers de memória não pertencentes ao código. Adicionalmente, eles não podem executar operações que poderiam ter um efeito adverso na robustez do processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]  
  
### <a name="unsafe"></a>UNSAFE  
 UNSAFE concede aos assemblies acesso irrestrito aos recursos, dentro e fora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Código executado em um assembly UNSAFE pode chamar código não gerenciado.  
  
 Além disso, especificando UNSAFE permite que o código no assembly execute operações consideradas como tipo inseguro pelo verificador CLR. Essas operações podem potencialmente acessar buffers de memória no espaço de processo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de uma maneira descontrolada. Assemblies UNSAFE também podem potencialmente subverter o sistema de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou do CLR. Somente permissões UNSAFE devem ser concedidas a assemblies altamente confiáveis por desenvolvedores ou administradores experientes. Somente membros do **sysadmin** função de servidor fixa pode criar assemblies UNSAFE.  
  
## <a name="restrictions-on-assemblies"></a>Restrições em assemblies  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] coloca certas restrições em código gerenciado em assemblies para verificar se eles podem ser executados de uma maneira segura e evolutiva. Isso significa que não são permitidas certas operações que podem comprometer a robustez do servidor em assemblies SAFE e EXTERNAL_ACCESS.  
  
### <a name="disallowed-custom-attributes"></a>Atributos personalizados não permitidos  
 Assemblies não podem ser anotados com os seguintes atributos personalizados:  
  
```  
System.ContextStaticAttribute  
System.MTAThreadAttribute  
System.Runtime.CompilerServices.MethodImplAttribute  
System.Runtime.CompilerServices.CompilationRelaxationsAttribute  
System.Runtime.Remoting.Contexts.ContextAttribute  
System.Runtime.Remoting.Contexts.SynchronizationAttribute  
System.Runtime.InteropServices.DllImportAttribute   
System.Security.Permissions.CodeAccessSecurityAttribute  
System.STAThreadAttribute  
System.ThreadStaticAttribute  
```  
  
 Adicionalmente, não podem ser anotados assemblies SAFE e EXTERNAL_ACCESS com os seguintes atributos personalizados:  
  
```  
System.Security.SuppressUnmanagedCodeSecurityAttribute  
System.Security.UnverifiableCodeAttribute  
```  
  
### <a name="disallowed-net-framework-apis"></a>APIs não permitidas do .NET Framework  
 Qualquer [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] API anotada com uma das proibições **HostProtectionAttributes** não pode ser chamado de assemblies SAFE e EXTERNAL_ACCESS.  
  
```  
eSelfAffectingProcessMgmt  
eSelfAffectingThreading  
eSynchronization  
eSharedState   
eExternalProcessMgmt  
eExternalThreading  
eSecurityInfrastructure  
eMayLeakOnAbort  
eUI  
```  
  
### <a name="supported-net-framework-assemblies"></a>Assemblies .NET Framework suportados  
 Qualquer assembly referenciado por seu assembly personalizado deve ser carregado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando CREATE ASSEMBLY. Os seguintes assemblies do [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)] já estão carregados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e, portanto, podem ser consultados por assemblies personalizados sem ter que usar CREATE ASSEMBLY.  
  
```  
custommarshallers.dll  
Microsoft.visualbasic.dll  
Microsoft.visualc.dll  
mscorlib.dll  
system.data.dll  
System.Data.SqlXml.dll  
system.dll  
system.security.dll  
system.web.services.dll  
system.xml.dll  
System.Transactions  
System.Data.OracleClient  
System.Configuration  
```  
  
## <a name="see-also"></a>Consulte também  
 [Assemblies &#40; mecanismo de banco de dados &#41;](../../relational-databases/clr-integration/assemblies-database-engine.md)   
 [Segurança da integração CLR](../../relational-databases/clr-integration/security/clr-integration-security.md)  
  
  
