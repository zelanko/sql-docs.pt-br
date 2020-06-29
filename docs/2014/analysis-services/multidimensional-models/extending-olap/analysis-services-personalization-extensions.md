---
title: Extensões de personalização de Analysis Services | Microsoft Docs
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
ms.openlocfilehash: 0cd36cb2882659bff902d9830af0c5acefd98444
ms.sourcegitcommit: 04ba0ed3d860db038078609d6e348b0650739f55
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/27/2020
ms.locfileid: "85468971"
---
# <a name="analysis-services-personalization-extensions"></a>Extensões de personalização do Analysis Services
  [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]as [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização são a base da ideia de implementar uma arquitetura de plug-in. Em uma arquitetura de plug-in, é possível desenvolver novos objetos de cubo e funcionalidades de modo dinâmico e compartilhá-los com outros desenvolvedores. Dessa forma, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as extensões de personalização fornecem a funcionalidade que torna possível obter o seguinte:  
  
-   **Design e implantação dinâmicos** Imediatamente depois de criar e implantar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização, os usuários têm acesso aos objetos e à funcionalidade no início da próxima sessão de usuário.  
  
-   **Independência de interface** Independentemente da interface que você usa para criar as [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização, os usuários podem usar qualquer interface para acessar os objetos e a funcionalidade.  
  
-   **Contexto** [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] da sessão as extensões de personalização não são objetos permanentes na infraestrutura existente e não exigem que o cubo seja reprocessado. Elas são expostas e criadas para o usuário quando ele se conecta ao banco de dados e permanecem disponíveis durante toda a sessão de usuário.  
  
-   **Distribuição rápida** Compartilhe [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] extensões de personalização com outros desenvolvedores de software sem precisar entrar em especificações detalhadas sobre onde ou como encontrar essa funcionalidade estendida.  
  
 As extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] têm muitos usos. Por exemplo, sua empresa faz vendas que envolvem moedas diferentes. Você cria um membro calculado que retorna as vendas consolidadas na moeda local da pessoa que está acessando o cubo. Esse membro é criado como uma extensão de personalização. Em seguida, esse membro calculado é compartilhado com um grupo de usuários. Uma vez compartilhado, esses usuários têm acesso imediato ao membro calculado assim que se conectam ao servidor. Eles têm acesso mesmo se não estiverem usando a mesma interface que foi usada para criar o membro calculado.  
  
 [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]as extensões de personalização são uma modificação simples e elegante da arquitetura de assembly gerenciada existente e são expostas em todo o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] modelo de objeto [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) , sintaxe MDX e conjuntos de linhas de esquema.  
  
## <a name="logical-architecture"></a>Arquitetura lógica  
 A arquitetura das extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] baseia-se na arquitetura de assemblies gerenciados e nos quatro elementos básicos a seguir:  
  
 O atributo personalizado [PlugInAttribute]  
 Ao iniciar o serviço, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o carrega os assemblies necessários e determina quais classes têm o atributo personalizado [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) .  
  
> [!NOTE]  
>  O [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] define atributos personalizados como um modo de descrever seu código e afetar comportamento em tempo de execução. Para obter mais informações, consulte o tópico "[visão geral de atributos](https://go.microsoft.com/fwlink/?LinkId=82929)" no [!INCLUDE[dnprdnshort](../../../includes/dnprdnshort-md.md)] Guia do desenvolvedor no msdn.  
  
 Para todas as classes com o atributo personalizado [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)) , [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] invoca seus construtores padrão. A invocação de todos os construtores na inicialização fornece um local comum a partir do qual serão criados novos objetos e que é independente de todas as atividades de usuário.  
  
 Além de criar um pequeno cache de informações sobre a criação e o gerenciamento de extensões de personalização, o construtor de classe normalmente assina os eventos [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) e [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . A não assinatura desses eventos pode fazer com que a classe seja marcada inadequadamente para ser limpa pelo coletor de lixo CLR (Common Language Runtime).  
  
 Contexto de sessão  
 Para os objetos baseados em extensões de personalização, o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] cria um ambiente de execução durante a sessão cliente e cria dinamicamente a maioria desses objetos nesse ambiente. Como qualquer outro assembly CLR, esse ambiente de execução também tem acesso a outras funções e procedimentos armazenados. Quando a sessão de usuário termina, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o Remove os objetos criados dinamicamente e fecha o ambiente de execução.  
  
 Eventos  
 A criação de objetos é acionada pelos eventos de sessão `On-Cube-OpenedCubeOpened` e `On-Cube-ClosingCubeClosing`.  
  
 A comunicação entre o cliente e o servidor acontece através de eventos específicos. Esses eventos alertam o cliente sobre as situações que levam à criação de objetos do cliente. O ambiente do cliente é criado dinamicamente com dois conjuntos de eventos: eventos de sessão e eventos de cubo.  
  
 Os eventos de sessão são associados ao objeto de servidor. Quando um cliente faz logon em um servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] o cria uma sessão e dispara o evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) . Quando um cliente encerra a sessão no servidor, [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dispara o evento [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120)) .  
  
 Os eventos de cubo são associados ao objeto de conexão. Conectar-se a um cubo dispara o evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120)) . Fechar a conexão com um cubo, fechando o cubo ou alterando para um cubo diferente, dispara um evento [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120)) .  
  
 Rastreamento e manipulação de erros  
 Todas as atividades podem ser rastreadas com [!INCLUDE[ssSqlProfiler](../../../includes/sssqlprofiler-md.md)]. Os erros não manipulados são relatados no log de evento do Windows.  
  
 Todas as atividades de criação e gerenciamento de objetos são independentes dessa arquitetura são de responsabilidade exclusiva dos desenvolvedores dos objetos.  
  
## <a name="infrastructure-foundations"></a>Base da infraestrutura  
 As extensões de personalização do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] baseiam-se em componentes existentes. Veja, a seguir, um resumo de aprimoramentos e melhorias que fornecem a funcionalidade de extensões de personalização.  
  
### <a name="assemblies"></a>Assemblies  
 O atributo personalizado, [Microsoft. AnalysisServices. AdomdServer. PlugInAttribute](/previous-versions/sql/sql-server-2014/bb678014(v=sql.120)), pode ser adicionado aos assemblies personalizados para identificar [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] as classes de extensões de personalização.  
  
### <a name="changes-to-the-adomdserver-object-model"></a>Alterações no modelo de objeto AdomdServer  
 Os objetos a seguir no modelo de objeto [Microsoft. AnalysisServices. AdomdServer](/previous-versions/sql/sql-server-2014/ms131779(v=sql.120)) foram aprimorados ou adicionados ao modelo.  
  
#### <a name="new-adomdconnection-class"></a>Nova classe AdomdConnection  
 A classe [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) é nova e expõe várias extensões de personalização por meio de propriedades e eventos.  
  
 **Propriedades**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. SessionID *](/previous-versions/sql/sql-server-2014/bb678099(v=sql.120)), um valor de cadeia de caracteres somente leitura que representa a ID de sessão da conexão atual.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. ClientCulture *](/previous-versions/sql/sql-server-2014/bb677433(v=sql.120)), uma referência somente leitura à cultura do cliente associada à sessão atual.  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. User *](/previous-versions/sql/sql-server-2014/bb630315(v=sql.120)), uma referência somente leitura para a interface de identidade que representa o usuário atual.  
  
 **Eventos**  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeOpened](/previous-versions/sql/sql-server-2014/bb630581(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. AdomdConnection. CubeClosing](/previous-versions/sql/sql-server-2014/bb630371(v=sql.120))  
  
#### <a name="new-properties-in-the-context-class"></a>Novas propriedades na classe Context  
 A classe [Microsoft. AnalysisServices. AdomdServer. Context](/previous-versions/sql/sql-server-2014/ms143353(v=sql.120)) tem duas novas propriedades:  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. Server *](/previous-versions/sql/sql-server-2014/bb678098(v=sql.120)), uma referência somente leitura para o novo objeto de servidor.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Context. CurrentConnection *](/previous-versions/sql/sql-server-2014/bb630975(v=sql.120)), uma referência somente leitura para o novo objeto [Microsoft. AnalysisServices. AdomdServer. AdomdConnection](/previous-versions/sql/sql-server-2014/bb678193(v=sql.120)) .  
  
#### <a name="new-server-class"></a>Nova classe Server  
 A classe [Microsoft. AnalysisServices. AdomdServer. Server](/previous-versions/sql/sql-server-2014/bb677955(v=sql.120)) é nova e expõe várias extensões de personalização por meio de propriedades de classe e eventos.  
  
 **Propriedades**  
  
-   [Microsoft.AnalysisServices.AdomdServer.Server.Name *](/previous-versions/sql/sql-server-2014/bb677694(v=sql.120)), um valor de cadeia de caracteres somente leitura que representa o nome do servidor.  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. Culture *](/previous-versions/sql/sql-server-2014/bb677437(v=sql.120)), uma referência somente leitura para a cultura global associada ao servidor.  
  
 **Eventos**  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionOpened](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
-   [Microsoft. AnalysisServices. AdomdServer. Server. SessionClosing](/previous-versions/sql/sql-server-2014/bb630427(v=sql.120))  
  
#### <a name="adomdcommand-class"></a>Classe AdomdCommand  
 A classe [Microsoft. AnalysisServices. AdomdServer. AdomdCommand](/previous-versions/sql/sql-server-2014/ms143286(v=sql.120)) agora dá suporte aos seguintes comandos MDX:  
  
-   [Instrução CREATE MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-member)  
  
-   [ATUALIZAR a instrução de membro &#40;MDX&#41;](/sql/mdx/mdx-data-definition-update-member)  
  
-   [Instrução DROP MEMBER &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-member)  
  
-   [Instrução CREATE SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-set)  
  
-   [Instrução DROP SET &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-set)  
  
-   [Instrução CREATE KPI &#40;MDX&#41;](/sql/mdx/mdx-data-definition-create-kpi)  
  
-   [Instrução DROP KPI &#40;MDX&#41;](/sql/mdx/mdx-data-definition-drop-kpi)  
  
### <a name="mdx-extensions-and-enhancements"></a>Extensões e aprimoramentos MDX  
 O comando CREATE MEMBER foi aprimorado com as propriedades `caption`, `display_folder` e `associated_measure_group`.  
  
 O comando UPDATE MEMBER foi adicionado para evitar a recriação de membros quando uma atualização é necessária com a perda de precedência resultante na solução de cálculos. As atualizações não podem alterar o escopo do membro calculado, mover o membro calculado para um pai diferente ou definir um `solveorder` diferente.  
  
 O comando CREATE SET foi aprimorado com as propriedades `caption` e `display_folder` e a nova palavra-chave `STATIC | DYNAMIC`. *Static* significa que Set é avaliado somente no momento da criação. *Dinâmico* significa que o conjunto é avaliado toda vez que o conjunto é usado em uma consulta. O valor padrão será `STATIC` se uma palavra-chave for omitida.  
  
 Os comandos CREATE KPI e DROP KPI foram adicionados à sintaxe MDX. KPIs podem ser criados dinamicamente a partir de qualquer script MDX.  
  
### <a name="schema-rowsets-extensions"></a>Extensões de conjuntos de linhas de esquema  
 Na coluna *escopo* MDSCHEMA_MEMBERS é adicionada. Os valores de escopo são: MDMEMBER_SCOPE_GLOBAL = 1, MDMEMBER_SCOPE_SESSION = 2.  
  
 Na coluna MDSCHEMA_SETS *set_evaluation_context* é adicionada. Defina os valores de contexto de avaliação do seguinte modo: MDSET_RESOLUTION_STATIC = 1, MDSET_RESOLUTION_DYNAMIC = 2.  
  
 Em MDSCHEMA_KPIS, a coluna de escopo foi adicionada. Os valores de escopo são: MDKPI_SCOPE_GLOBAL = 1, MDKPI_SCOPE_SESSION = 2.  
  
  
