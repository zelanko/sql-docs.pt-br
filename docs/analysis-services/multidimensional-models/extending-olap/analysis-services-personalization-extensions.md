---
title: "Extensões de personalização do Analysis Services | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
- docset-sql-devref
ms.tgt_pltfrm: 
ms.topic: reference
applies_to:
- SQL Server 2016 Preview
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
caps.latest.revision: 22
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 8da5ac35a5e9f46fbaedf831555d6b1475b41234
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="analysis-services-personalization-extensions"></a>Extensões de personalização do Analysis Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)][!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização são a base do conceito de implementação de uma arquitetura de plug-in. Em uma arquitetura de plug-in, é possível desenvolver novos objetos de cubo e funcionalidades de modo dinâmico e compartilhá-los com outros desenvolvedores. Como tal, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização fornecem a funcionalidade que possibilita fazer o seguinte:  
  
-   **Projeto e implantação dinâmicos** imediatamente depois de projetar e implantar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização, os usuários têm acesso a objetos e funcionalidade no início da próxima sessão de usuário.  
  
-   **Independência da interface** independentemente da interface que você usa para criar o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização, os usuários podem usar qualquer interface para acessar os objetos e funcionalidade.  
  
-   **Contexto de sessão** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização não são objetos permanentes na infraestrutura existente e não requerem o cubo seja reprocessado. Elas são expostas e criadas para o usuário quando ele se conecta ao banco de dados e permanecem disponíveis durante toda a sessão de usuário.  
  
-   **Rápida distribuição** compartilhamento [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] estendidos de extensões de personalização com outros desenvolvedores de software sem precisar fornecer especificações detalhadas sobre onde ou como encontrar essa funcionalidade.  
  
 As extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] têm muitos usos. Por exemplo, sua empresa faz vendas que envolvem moedas diferentes. Você cria um membro calculado que retorna as vendas consolidadas na moeda local da pessoa que está acessando o cubo. Esse membro é criado como uma extensão de personalização. Em seguida, esse membro calculado é compartilhado com um grupo de usuários. Uma vez compartilhado, esses usuários têm acesso imediato ao membro calculado assim que eles se conectam ao servidor. Eles têm acesso mesmo se não estiverem usando a mesma interface que foi usada para criar o membro calculado.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]extensões de personalização fazem uma modificação simple e discreta na arquitetura de assemblies gerenciados existente e são expostas em todo o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> modelo, sintaxe de MDX (Multidimensional Expressions) e conjuntos de linhas do esquema do objeto.  
  
## <a name="logical-architecture"></a>Arquitetura lógica  
 A arquitetura das extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] baseia-se na arquitetura de assemblies gerenciados e nos quatro elementos básicos a seguir:  
  
 O atributo personalizado [PlugInAttribute]  
 Ao iniciar o serviço, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carrega os assemblies necessários e determina quais classes têm o <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado.  
  
> [!NOTE]  
>  O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] define atributos personalizados como um modo de descrever seu código e afetar comportamento em tempo de execução. Para obter mais informações, consulte o tópico "[visão geral de atributos](http://go.microsoft.com/fwlink/?LinkId=82929)," no [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] guia do desenvolvedor do MSDN.  
  
 Para todas as classes com o <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] invoca seus construtores padrão. Invocar todos os construtores na inicialização fornece um local comum para criar novos objetos e que é independente de qualquer atividade de usuário.  
  
 Além de criar um pequeno cache de informações sobre a geração e o gerenciamento de extensões de personalização, o construtor de classe normalmente assina os eventos <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> e <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>. A não assinatura desses eventos pode fazer com que a classe seja marcada inadequadamente para ser limpa pelo coletor de lixo CLR (Common Language Runtime).  
  
 Contexto de sessão  
 Para os objetos baseados em extensões de personalização, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria um ambiente de execução durante a sessão cliente e cria dinamicamente a maioria desses objetos nesse ambiente. Como qualquer outro assembly CLR, esse ambiente de execução também tem acesso a outras funções e procedimentos armazenados. Quando termina a sessão do usuário, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] remove os objetos criados dinamicamente e fecha o ambiente de execução.  
  
 Eventos  
 Criação de objeto é acionada pelos eventos de sessão **OpenedCubeOpened no cubo** e **ClosingCubeClosing no cubo**.  
  
 A comunicação entre o cliente e o servidor acontece através de eventos específicos. Esses eventos alertam o cliente sobre as situações que levam à criação de objetos do cliente. O ambiente do cliente é criado dinamicamente com dois conjuntos de eventos: eventos de sessão e eventos de cubo.  
  
 Os eventos de sessão são associados ao objeto de servidor. Quando um cliente efetua logon em um servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria uma sessão e aciona o <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> evento. Quando um cliente termina a sessão no servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] gatilhos o <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> evento.  
  
 Os eventos de cubo são associados ao objeto de conexão. A conexão a um cubo aciona o evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>. O encerramento da conexão com um cubo, seja fechando o cubo ou mudando para um cubo diferente, aciona um evento <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>.  
  
 Rastreamento e manipulação de erros  
 Todas as atividades podem ser rastreadas com [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Os erros não manipulados são relatados no log de evento do Windows.  
  
 Todas as atividades de criação e gerenciamento de objetos são independentes dessa arquitetura são de responsabilidade exclusiva dos desenvolvedores dos objetos.  
  
## <a name="infrastructure-foundations"></a>Base da infraestrutura  
 As extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] baseiam-se em componentes existentes. Veja, a seguir, um resumo de aprimoramentos e melhorias que fornecem a funcionalidade de extensões de personalização.  
  
### <a name="assemblies"></a>Assemblies  
 O atributo personalizado, <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute>, pode ser adicionado aos seus assemblies personalizados para identificar as classes de extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Alterações no modelo de objeto AdomdServer  
 Os objetos a seguir do modelo de objeto <xref:Microsoft.AnalysisServices.AdomdServer> foram aprimorados ou adicionados ao modelo.  
  
#### <a name="new-adomdconnection-class"></a>Nova classe AdomdConnection  
 A classe <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection> é nova e expõe várias extensões de personalização por propriedades e eventos.  
  
 **Propriedades**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.SessionID%2A>, um valor de cadeia de caracteres somente leitura que representa a ID de sessão da conexão atual.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.ClientCulture%2A>, uma referência somente leitura para a cultura de cliente associada à sessão atual.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.User%2A>, uma referência somente leitura para a interface de identidade que representa o usuário atual.  
  
 **Eventos**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection.CubeClosing>  
  
#### <a name="new-properties-in-the-context-class"></a>Novas propriedades na classe Context  
 A classe <xref:Microsoft.AnalysisServices.AdomdServer.Context> tem duas propriedades novas:  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.Server%2A>, uma referência somente leitura para o novo objeto de servidor.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Context.CurrentConnection%2A>, uma referência somente leitura para o novo objeto <xref:Microsoft.AnalysisServices.AdomdServer.AdomdConnection>.  
  
#### <a name="new-server-class"></a>Nova classe Server  
 A classe <xref:Microsoft.AnalysisServices.AdomdServer.Server> é nova e expõe várias extensões de personalização por propriedades e eventos de classe.  
  
 **Propriedades**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Name%2A>, um valor de cadeia de caracteres somente leitura que representa o nome do servidor.  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.Culture%2A>, uma referência somente leitura para a cultura global associada ao servidor.  
  
 **Eventos**  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened>  
  
-   <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>  
  
#### <a name="adomdcommand-class"></a>Classe AdomdCommand  
 A classe <xref:Microsoft.AnalysisServices.AdomdServer.AdomdCommand> agora dá suporte aos seguintes comandos MDX:  
  
-   [Instrução CREATE MEMBER &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-member.md)  
  
-   [Declaração de membro UPDATE &#40; MDX &#41;](../../../mdx/mdx-data-definition-update-member.md)  
  
-   [Remover membro instrução &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-member.md)  
  
-   [Instrução CREATE SET &#40;MDX&#41;](../../../mdx/mdx-data-definition-create-set.md)  
  
-   [Remova a instrução SET &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-set.md)  
  
-   [Criar KPI instrução &#40; MDX &#41;](../../../mdx/mdx-data-definition-create-kpi.md)  
  
-   [Instrução DROP KPI retorna &#40; MDX &#41;](../../../mdx/mdx-data-definition-drop-kpi.md)  
  
### <a name="mdx-extensions-and-enhancements"></a>Extensões e aprimoramentos MDX  
 O comando CREATE MEMBER foi aprimorado com o **legenda** propriedade, o **display_folder** propriedade e o **associated_measure_group** propriedade.  
  
 O comando UPDATE MEMBER foi adicionado para evitar a recriação de membros quando uma atualização é necessária com a perda de precedência resultante na solução de cálculos. Atualizações não é possível alterar o escopo do membro calculado, mover o membro calculado para um pai diferente ou definir outro **solveorder**.  
  
 O comando CREATE SET foi aprimorado com o **legenda** propriedade, o **display_folder** propriedade e o novo **estático | DINÂMICO** palavra-chave. *Estático* significa que o conjunto é avaliado somente no momento da criação. *Dinâmico* significa que o conjunto é avaliado toda vez que o conjunto é usado em uma consulta. O valor padrão é **estático** se uma palavra-chave for omitida.  
  
 Os comandos CREATE KPI e DROP KPI foram adicionados à sintaxe MDX. KPIs podem ser criados dinamicamente a partir de qualquer script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Extensões de conjuntos de linhas de esquema  
 Em MDSCHEMA_MEMBERS *escopo* coluna é adicionada. Os valores de escopo são: MDMEMBER_SCOPE_GLOBAL = 1, MDMEMBER_SCOPE_SESSION = 2.  
  
 Em MDSCHEMA_SETS *set_evaluation_context* coluna é adicionada. Defina os valores de contexto de avaliação do seguinte modo: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 Em MDSCHEMA_KPIS, a coluna de escopo foi adicionada. Os valores de escopo são: MDKPI_SCOPE_GLOBAL = 1, MDKPI_SCOPE_SESSION = 2.  
  
  

