---
title: Extensões de personalização do Analysis Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: reference
helpviewer_keywords:
- personalization extensions [Multidimensional Databases]
ms.assetid: 0f144059-24e0-40c0-bde4-d48c75e46598
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 313b1764dfb17c3a8b49fa3ffa139668f9b2b421
ms.sourcegitcommit: b87c384e10d6621cf3a95ffc79d6f6fad34d420f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "60156253"
---
# <a name="analysis-services-personalization-extensions"></a>Extensões de personalização do Analysis Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização são a base do conceito de implementar uma arquitetura de plug-in. Em uma arquitetura de plug-in, é possível desenvolver novos objetos de cubo e funcionalidades de modo dinâmico e compartilhá-los com outros desenvolvedores. Como tal, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização fornecem a funcionalidade que possibilita fazer o seguinte:  
  
-   **Design dinâmico e a implantação** imediatamente depois de projetar e implantar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização, os usuários têm acesso a objetos e funcionalidades no início da próxima sessão de usuário.  
  
-   **Independência da interface** independentemente da interface que você pode usar para criar o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização, os usuários podem usar qualquer interface para acessar os objetos e funcionalidade.  
  
-   **Contexto de sessão** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização não são objetos permanentes na infraestrutura existente e não exigem o cubo para ser reprocessadas. Elas são expostas e criadas para o usuário quando ele se conecta ao banco de dados e permanecem disponíveis durante toda a sessão de usuário.  
  
-   **Rápida distribuição** compartilhamento [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] funcionalidade estendida de extensões de personalização com outros desenvolvedores de software sem precisar entrar em especificações detalhadas sobre onde ou como encontrá-lo.  
  
 As extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] têm muitos usos. Por exemplo, sua empresa faz vendas que envolvem moedas diferentes. Você cria um membro calculado que retorna as vendas consolidadas na moeda local da pessoa que está acessando o cubo. Esse membro é criado como uma extensão de personalização. Em seguida, esse membro calculado é compartilhado com um grupo de usuários. Uma vez compartilhado, esses usuários têm acesso imediato ao membro calculado assim que eles se conectam ao servidor. Eles têm acesso mesmo se não estiverem usando a mesma interface que foi usada para criar o membro calculado.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização fazem uma modificação simples e discreta na arquitetura do assembly gerenciado existente e são expostas em todo o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] <xref:Microsoft.AnalysisServices.AdomdServer> modelo, a sintaxe de MDX (Multidimensional Expressions) e conjuntos de linhas de esquema do objeto.  
  
## <a name="logical-architecture"></a>Arquitetura lógica  
 A arquitetura das extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] baseia-se na arquitetura de assemblies gerenciados e nos quatro elementos básicos a seguir:  
  
 O atributo personalizado [PlugInAttribute]  
 Ao iniciar o serviço [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] carrega os assemblies necessários e determina quais classes têm o <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado.  
  
> [!NOTE]  
>  O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] define atributos personalizados como um modo de descrever seu código e afetar comportamento em tempo de execução. Para obter mais informações, consulte o tópico "[visão geral de atributos](https://go.microsoft.com/fwlink/?LinkId=82929)," no [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] guia do desenvolvedor do MSDN.  
  
 Para todas as classes com o <xref:Microsoft.AnalysisServices.AdomdServer.PlugInAttribute> atributo personalizado, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] invoca seus construtores padrão. Invocação de todos os construtores na inicialização fornece um local comum para criar novos objetos e que é independente de qualquer atividade de usuário.  
  
 Além de criar um pequeno cache de informações sobre a geração e o gerenciamento de extensões de personalização, o construtor de classe normalmente assina os eventos <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> e <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing>. A não assinatura desses eventos pode fazer com que a classe seja marcada inadequadamente para ser limpa pelo coletor de lixo CLR (Common Language Runtime).  
  
 Contexto de sessão  
 Para os objetos baseados em extensões de personalização, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria um ambiente de execução durante a sessão cliente e cria dinamicamente a maioria desses objetos nesse ambiente. Como qualquer outro assembly CLR, esse ambiente de execução também tem acesso a outras funções e procedimentos armazenados. Quando termina a sessão do usuário, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] remove os objetos criados dinamicamente e fecha o ambiente de execução.  
  
 Eventos  
 A criação de objetos é acionada pelos eventos de sessão `On-Cube-OpenedCubeOpened` e `On-Cube-ClosingCubeClosing`.  
  
 A comunicação entre o cliente e o servidor acontece através de eventos específicos. Esses eventos alertam o cliente sobre as situações que levam à criação de objetos do cliente. O ambiente do cliente é criado dinamicamente com dois conjuntos de eventos: eventos de sessão e eventos de cubo.  
  
 Os eventos de sessão são associados ao objeto de servidor. Quando um cliente efetua logon em um servidor [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria uma sessão e aciona o <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionOpened> eventos. Quando um cliente encerra a sessão no servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] gatilhos a <xref:Microsoft.AnalysisServices.AdomdServer.Server.SessionClosing> eventos.  
  
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
  
-   [Instrução CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [Declaração de membro de UPDATE &#40;MDX&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [Instrução de membro DROP &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [Instrução CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [Instrução SET no menu &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [Instrução CREATE KPI &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [Instrução do DROP KPI &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>Extensões e aprimoramentos MDX  
 O comando CREATE MEMBER foi aprimorado com as propriedades `caption`, `display_folder` e `associated_measure_group`.  
  
 O comando UPDATE MEMBER foi adicionado para evitar a recriação de membros quando uma atualização é necessária com a perda de precedência resultante na solução de cálculos. As atualizações não podem alterar o escopo do membro calculado, mover o membro calculado para um pai diferente ou definir um `solveorder` diferente.  
  
 O comando CREATE SET foi aprimorado com as propriedades `caption` e `display_folder` e a nova palavra-chave `STATIC | DYNAMIC`. *Estático* significa que o conjunto é avaliado somente no momento da criação. *Dinâmico* significa que o conjunto é avaliado toda vez que o conjunto é usado em uma consulta. O valor padrão será `STATIC` se uma palavra-chave for omitida.  
  
 Os comandos CREATE KPI e DROP KPI foram adicionados à sintaxe MDX. KPIs podem ser criados dinamicamente a partir de qualquer script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Extensões de conjuntos de linhas de esquema  
 Em MDSCHEMA_MEMBERS *escopo* coluna é adicionada. Valores de escopo são da seguinte maneira: MDMEMBER_SCOPE_GLOBAL=1, MDMEMBER_SCOPE_SESSION=2.  
  
 Em MDSCHEMA_SETS *set_evaluation_context* coluna é adicionada. Defina o contexto de avaliação, os valores são da seguinte maneira: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 Em MDSCHEMA_KPIS, a coluna de escopo foi adicionada. Valores de escopo são da seguinte maneira: MDKPI_SCOPE_GLOBAL=1, MDKPI_SCOPE_SESSION=2.  
  
  
