---
title: Gerenciamento de assemblies de modelo multidimensional | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- permissions [Analysis Services], assemblies
- calling user-defined functions
- user impersonation [Analysis Services]
- impersonation [Analysis Services]
- Data Mining Extensions [Analysis Services], assemblies
- MDX [Analysis Services], assemblies
- user-defined functions [Analysis Services]
- Analysis Services objects, assemblies
- assemblies [Analysis Services]
- application domains [Analysis Services]
ms.assetid: b2645d10-6d17-444e-9289-f111ec48bbfb
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 6c4f57e12754fc8e32fba8f483a2dfc360d7edc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66073525"
---
# <a name="multidimensional-model-assemblies-management"></a>Gerenciamento de assemblies de modelo multidimensional
  [!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece muitas funções intrínsecas para uso com as linguagens MDX (Multidimensional Expressions) e DMX (Data Mining Extensions), projetadas para realizar tudo, desde cálculos estatísticos padrão até a passagem de membros em uma [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] hierarquia. Mas, como em qualquer outro produto complexo, há sempre a necessidade de estender a funcionalidade para o produto.  
  
 Portanto, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] permite adicionar assemblies a uma instância ou banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Os assemblies permitem criar funções externas definidas pelo usuário usando qualquer CLR (Common Language Runtime), como o Microsoft Visual Basic .NET ou o Microsoft Visual C#. Você também pode usar linguagens de automação COM (Component Object Model), como o Microsoft Visual Basic ou o Microsoft Visual C++.  
  
> [!IMPORTANT]  
>  Os assemblies COM podem representar um risco à segurança. Devido a esse risco e outras considerações, os assemblies COM foram preteridos no [!INCLUDE[ssASversion10](../../includes/ssasversion10-md.md)]. Talvez não haja suporte para assemblies COM em versões futuras.  
  
 Os assemblies permitem estender a funcionalidade empresarial de MDX e DMX. É possível criar a funcionalidade desejada em uma biblioteca, como uma DLL (biblioteca de vínculo dinâmico) e adicionar a biblioteca como um assembly a uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou a um banco de dados do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Em seguida, os métodos públicos na biblioteca são expostos como funções definidas pelo usuário para expressões MDX e DMX, procedimentos, cálculos, ações e aplicativos cliente.  
  
 Um assembly com novos procedimentos e funções pode ser adicionado ao servidor. É possível usar assemblies para aprimorar ou adicionar funcionalidade personalizada que não foi fornecida pelo servidor. Usando os assemblies, você pode adicionar novas funções para o MDX, extensões DMX ou procedimentos armazenados. Os assemblies são carregados do local onde o aplicativo personalizado é executado e uma cópia do arquivo binário do assembly é salva com os dados do banco de dados no servidor. Quando um assembly é removido, o assembly copiado também é removido do servidor.  
  
 Os assemblies podem ser de dois tipos diferentes: COM e CLR. Os assemblies CLR são desenvolvidos em linguagens de programação .NET Framework, como C#, Visual Basic .NET, C++ gerenciado. Os assemblies COM são bibliotecas COM que devem ser registradas no servidor.  
  
 Assemblies podem ser adicionados a objetos <xref:Microsoft.AnalysisServices.Server> ou <xref:Microsoft.AnalysisServices.Database> . Os assemblies de servidor podem ser chamados por qualquer usuário conectado ao servidor ou qualquer objeto no servidor. Os assemblies de banco de dados só podem ser chamados por objetos <xref:Microsoft.AnalysisServices.Database> ou usuários conectados ao banco de dados.  
  
 Um objeto <xref:Microsoft.AnalysisServices.Assembly> simples é composto por informações básicas (Nome e ID), coleção de arquivos e especificações de segurança.  
  
 A coleção de arquivo refere-se aos arquivos assembly carregados e seus arquivos de depuração correspondentes (.pdb), caso os arquivos de depuração tenham sido carregados com os arquivos assembly. Os arquivos assembly são carregados do local em que o aplicativo definiu os arquivos e uma cópia é gravada no servidor com os dados. A cópia do arquivo assembly é usada para carregar o assembly sempre que o serviço é iniciado.  
  
 As especificações de segurança incluem a permissão definida e a representação usada para executar o assembly.  
  
## <a name="calling-user-defined-functions"></a>Chamando funções definidas pelo usuário  
 A chamada de uma função definida pelo usuário em um assembly é executada como a chamada de uma função intrínseca, exceto pelo fato de que você deve usar um nome totalmente qualificado. Por exemplo, uma função definida pelo usuário que retorna um tipo esperado pelo MDX é incluída em uma consulta MDX, conforme mostrado no exemplo a seguir:  
  
```  
Select MyAssembly.MyClass.MyStoredProcedure(a, b, c) on 0 from Sales  
```  
  
 As funções definidas pelo usuário também podem ser chamadas usando a palavra-chave CALL. Você deve usar a palavra-chave CALL para funções definidas pelo usuário que retornem conjuntos de registros ou valores nulos e não será possível usar a palavra-chave CALL se a função definida pelo usuário depender de um objeto no contexto da instrução ou script MDX ou DMX, como o cubo atual ou o modelo de mineração de dados. Um uso comum de uma função chamada fora de uma consulta MDX ou DMX é usar o modelo de objeto AMO para executar funções administrativas. Se, por exemplo, você quiser usar a função `MyVoidProcedure(a, b, c)` em uma instrução MDX, a seguinte sintaxe será aplicada:  
  
```  
Call MyAssembly.MyClass.MyVoidProcedure(a, b, c)  
```  
  
 Os assemblies simplificam o desenvolvimento de banco de dados, ativando o código comum a ser desenvolvido uma vez e armazenado em um único local. Os desenvolvedores de software cliente podem criar bibliotecas de funções para o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] e distribuí-las com seus aplicativos.  
  
 Os assemblies e funções definidas pelo usuário podem duplicar os nomes de função da biblioteca de funções do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ou de outros assemblies. Desde que você possa chamar a função definida pelo usuário usando seu nome totalmente qualificado, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] usará o procedimento correto. Para fins de segurança, e para eliminar a chance de chamar um nome duplicado em uma biblioteca de classes diferente, o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] requer que você use apenas nomes totalmente qualificados para procedimentos armazenados.  
  
 Para chamar uma função definida pelo usuário de um assembly CLR específico, a função é precedida pelo nome do assembly, o nome completo da classe e o nome do procedimento, conforme demonstrado aqui:  
  
 *AssemblyName*. *FullClassName*. *ProcedureName*(*argument1*, *argument2*,...)  
  
 Para fins de compatibilidade com versões anteriores do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a sintaxe a seguir é também aceitável:  
  
 *AssemblyName*! *FullClassName*! *ProcedureName*(*argument1*, *argument2*,...)  
  
 Se a biblioteca COM oferece suporte para várias interfaces, a ID da interface também pode ser usada para resolver o nome do procedimento, conforme demonstrado aqui:  
  
 *AssemblyName*! *InterfaceName*! *ProcedureName*(*argument1*, *argument2*,...)  
  
## <a name="security"></a>Segurança  
 A segurança dos assemblies baseia-se no modelo de segurança .NET Framework, que é um modelo de segurança de acesso por código. O .NET Framework oferece suporte a um mecanismo de segurança de acesso por código assumindo que o runtime pode hospedar tanto o código totalmente confiável quanto o parcialmente confiável. Os recursos protegidos pela segurança de código de acesso .NET Framework geralmente são envolvidos pelo código gerenciado que demanda a permissão correspondente antes de permitir o acesso ao recurso. A demanda para a permissão é satisfatória apenas quando todos os chamadores (no nível de assembly) na pilha de chamadas tiverem a permissão do recurso correspondente.  
  
 Para os assemblies, a permissão de execução é passada com a propriedade `PermissionSet` no objeto `Assembly`. As permissões que o código gerenciado recebe são determinadas pela política de segurança em vigor. Existem três níveis de política que estão em vigor em um ambiente de host não[!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] : empresa, computador e usuário. A lista efetiva de permissões que o código recebe é determinada pela interseção das permissões obtidas por esses três níveis.  
  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] fornece um nível de política de segurança no nível do host ao CLR ao hospedá-lo; essa política é um nível de política adicional abaixo dos três níveis de política que estão sempre em funcionamento. Essa política é definida para todos os domínios de aplicativo criados pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)].  
  
 A política de nível host do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] é uma combinação de política fixa do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] para assemblies de sistema e política específica de usuário para assemblies de usuário. A parte especificada pelo usuário da política host do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] baseia-se no proprietário do assembly especificando um de três recipientes de permissão para cada assembly.  
  
|Configuração de permissões|DESCRIÇÃO|  
|------------------------|-----------------|  
|`Safe`|Fornece a permissão de computação interna. Esse recipiente de permissão não atribui permissões para acessar qualquer um dos recursos protegidos em .NET Framework. Este será o recipiente de permissão padrão de um assembly se não houver outro especificado com a propriedade `PermissionSet`.|  
|`ExternalAccess`|Fornece o mesmo acesso que a configuração `Safe`, com a habilidade adicional de acessar recursos externos do sistema. Esse recipiente de permissão não oferece garantias de segurança (embora seja possível para proteger esse cenário), mas oferece garantias de confiabilidade.|  
|`Unsafe`|Não fornece restrições. Nenhuma garantia de segurança ou confiabilidade pode ser criada para o código gerenciado executado sob essa permissão definida. Qualquer permissão, mesmo uma permissão personalizada incluída pelo administrador, é concedida ao código executado nesse nível de confiança.|  
  
 Quando o CLR é hospedado pelo [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], a permissão com base em fila verifica interrupções no limite com o código nativo do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Qualquer código gerenciado em assemblies [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] sempre entra em uma das três categorias de permissão listadas anteriormente.  
  
 As rotinas de assembly COM (ou não gerenciadas) não oferecem suporte ao modelo de segurança CLR.  
  
### <a name="impersonation"></a>Representação  
 Sempre que o código gerenciado acessa qualquer recurso fora do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] segue as regras associadas à configuração da propriedade `ImpersonationMode` do assembly para certificar-se de que o acesso ocorre em um contexto de segurança apropriado do Windows. Como os assemblies que usam a configuração de permissão `Safe` não podem acessar recursos fora do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], essas regras são aplicáveis apenas aos assemblies, usando as configurações de permissão `ExternalAccess` e `Unsafe`.  
  
-   Se o contexto de execução atual corresponder ao logon autenticado do Windows e for o mesmo que o contexto do chamador original (ou seja, sem EXECUTE AS no meio), o [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] representará o logon autenticado do Windows antes de acessar o recurso.  
  
-   Se houver um EXECUTE AS intermediário que altere o contexto do chamador original, a tentativa de acessar o recurso externo falhará.  
  
 A propriedade `ImpersonationMode` pode ser definida como `ImpersonateCurrentUser` ou `ImpersonateAnonymous`. A configuração padrão, `ImpersonateCurrentUser`, executa um assembly na conta de login de rede do usuário atual. Se a `ImpersonateAnonymous` configuração for usada, o contexto de execução será correspondente à conta de*usuário de logon do Windows IUSER_* ServerName no servidor. Esta é a conta-convidado da Internet que limitou os privilégios no servidor. Um assembly executado nesse contexto só pode acessar recursos limitados no servidor local.  
  
### <a name="application-domains"></a>Domínios de aplicativo  
 
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] não expõe os domínios de aplicativo diretamente. Devido a um conjunto de assemblies executado no mesmo domínio de aplicativo, os domínios de aplicativo podem descobrir um ao outro no momento de execução usando o namespace `System.Reflection` no .NET Framework, ou de alguma outra maneira, e podem chamá-los no modo associado mais recente. Essa chamadas estarão sujeitas às verificações de permissão usadas pela segurança com base na autorização do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 Você não deve confiar na localização dos assemblies no mesmo domínio do aplicativo, pois o limite do domínio de aplicativo e dos assemblies que vão para cada domínio são definidos pela implementação.  
  
## <a name="see-also"></a>Consulte Também  
 [Definindo a segurança para procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/setting-security-for-stored-procedures.md)   
 [Definindo procedimentos armazenados](../multidimensional-models-extending-olap-stored-procedures/defining-stored-procedures.md)  
  
  
