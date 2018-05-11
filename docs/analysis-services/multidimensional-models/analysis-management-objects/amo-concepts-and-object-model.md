---
title: Conceitos de AMO e o modelo de objeto | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: amo
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 1cf8cb9dede901ea96eb1f5ad4c40fa6edd54660
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="amo-concepts-and-object-model"></a>Conceitos e modelo de objeto AMO
  Este tópico fornece uma definição de Analysis Management Objects (AMO), como ele se relaciona com outras ferramentas e bibliotecas da arquitetura de [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]e uma explicação conceitual de todos os objetos principais AMO.  
  
 O AMO é uma coleção completa de classes de gerenciamento para o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] que pode ser usada programaticamente, sob o espaço para nome <xref:Microsoft.AnalysisServices>, em um ambiente gerenciado. As classes estão incluídas no arquivo AnalysisServices.dll, normalmente encontrado onde o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instalação instala os arquivos sob a pasta \100\SDK\Assemblies\\. Para usar as classes AMO, inclua uma referência a esse assembly em seus projetos.  
  
 Usando o AMO, você é capaz de criar, modificar e excluir objetos como cubos, dimensões, estruturas de mineração, e [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] bancos de dados; em todos esses objetos, ações podem ser executadas a partir de seu aplicativo no .NET Framework. Você também pode processar e atualizar as informações armazenadas em bancos de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
 Com o AMO, não é possível consultar os seus dados. Para consultar os dados, use [desenvolvendo com ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
 Este tópico contém as seguintes seções:  
  
 [AMO na arquitetura do Analysis Services](#AMOintheAnalysisServicesArchitecture)  
  
 [Arquitetura do AMO](#AMOArchitecture)  
  
 [Usando o AMO](#bkmk_UsingAMO)  
  
 [Automatizando tarefas administrativas com AMO](#AutomatingAdministrativeTaskswithAMO)  
  
##  <a name="AMOintheAnalysisServicesArchitecture"></a> AMO na arquitetura do Analysis Services  
 Por design, o AMO foi criado somente para o gerenciamento de objetos e não para a consulta de dados. Se o usuário precisa consulta [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] dados de um aplicativo cliente, o aplicativo cliente deve usar [desenvolvendo com ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
##  <a name="AMOArchitecture"></a> Arquitetura do AMO  
 O AMO é uma biblioteca de classes criada para gerenciar uma instância do completa [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] de um aplicativo cliente em código gerenciado no .NET Framework versão 2.0.  
  
 A biblioteca de classes AMO foi criada como uma hierarquia de classes, onde certas classes devem ser instanciadas antes de outras para que possam ser usadas em seu código. Existem também classes auxiliares que podem ser instanciadas em seu código em qualquer ocasião, mas provavelmente você instanciará uma ou mais das classes de hierarquia antes de usar qualquer uma delas.  
  
 A ilustração a seguir é uma exibição de alto nível da hierarquia AMO com as classes principais. A ilustração mostra o posicionamento das classes entre seus contêineres e entre seus pares. Um <xref:Microsoft.AnalysisServices.Dimension> pertence a um <xref:Microsoft.AnalysisServices.Database> e a um <xref:Microsoft.AnalysisServices.Server> e pode ser criado ao mesmo tempo do que um <xref:Microsoft.AnalysisServices.DataSource> e de um <xref:Microsoft.AnalysisServices.MiningStructure>. Certas classes pares devem ser instanciadas antes que outras possam ser usadas. Por exemplo, você precisa criar uma instância de <xref:Microsoft.AnalysisServices.DataSource> antes de adicionar um novo <xref:Microsoft.AnalysisServices.Dimension> ou um <xref:Microsoft.AnalysisServices.MiningStructure>.  
  
 ![Exibição de alto nível de Classes AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-highlevelview-majorobjectshighlighted.gif "AMO Classes de exibição de alto nível")  
  
 Um *objeto principal* é uma classe que representa um objeto completo como uma entidade completa e não como parte de outro objeto. Os objetos principais incluem <xref:Microsoft.AnalysisServices.Server>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.Dimension> e <xref:Microsoft.AnalysisServices.MiningStructure>, uma vez que essas são entidades autônomas. No entanto, um <xref:Microsoft.AnalysisServices.Level> não é um objeto principal, porque faz parte de um <xref:Microsoft.AnalysisServices.Dimension>. Os objetos principais podem ser criados, excluídos, modificados ou processados de forma independente de outros objetos. Os objetos menores são objetos que só podem ser criados como parte da criação do objeto principal pai. Normalmente, os objetos secundários são criados durante a criação de um objeto principal. Os valores dos objetos secundários devem ser definidos no momento de criação, uma vez que não há uma criação padrão para objetos secundários.  
  
 A ilustração a seguir mostra os objetos principais contidos por um <xref:Microsoft.AnalysisServices.Server>.  
  
 ![Objetos principais AMO destacados](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects.gif "objetos principais AMO destacados")  
  
 ![Objetos principais AMO destacados (2)](../../../analysis-services/multidimensional-models/analysis-management-objects/media/amo-majorobjects-02.gif "objetos principais AMO destacados (2)")  
  
 Na programação com AMO, a associação entre classes e classes contidas usa atributos de tipo de coleção, como por exemplo, <xref:Microsoft.AnalysisServices.Server> e <xref:Microsoft.AnalysisServices.Dimension>. Para trabalhar com uma instância de uma classe contida, primeiro adquira uma referência a um objeto de coleção que armazene e que possa armazenar a classe contida. Em seguida, localize o objeto específico que você está procurando na coleção para poder obter uma referência ao objeto para começar a trabalhar com ele.  
  
### <a name="amo-classes"></a>Classes AMO  
 O AMO é uma biblioteca de classes criada para gerenciar uma instância do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] a partir de um aplicativo cliente. A biblioteca AMO pode ser pensada como grupos de objetos usados na realização de uma tarefa específica. As classes AMO podem ser categorizadas da seguinte forma:  
  
|Conjunto de classes|Finalidade|  
|---------------|-------------|  
|[Classes fundamentais AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-fundamental-classes.md)|Classes necessárias para que seja possível trabalhar com outros conjuntos de classes.|  
|[Classes OLAP AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-olap-classes.md)|Classes que permitem a você gerenciar os objetos OLAP no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Classes de mineração de dados AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-data-mining-classes.md)|Classes que permitem a você gerenciar os objetos de mineração de dados no [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].|  
|[Classes de segurança AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-security-classes.md)|Classes que permitem a você controlar o acesso a outros objetos e a manter a segurança.|  
|[Outras classes e métodos AMO](../../../analysis-services/multidimensional-models/analysis-management-objects/amo-other-classes-and-methods.md)|Classes e métodos que ajudam os administradores de OLAP ou de mineração de dados a concluírem suas tarefas diárias.|  
  
##  <a name="bkmk_UsingAMO"></a> Usando o AMO  
 O AMO é especialmente útil para a automação de tarefas repetitivas, como por exemplo a criação de novas partições em um grupo de medidas baseado em dados novos da tabela de fatos, ou em um novo treinamento de um modelo de mineração baseado em dados novos. Essas tarefas que criam objetos novos são normalmente executadas por mês, por semana ou por trimestre, e os novos objetos podem ser facilmente nomeados, com base nos dados novos, pelo aplicativo.  
  
##### <a name="analysis-services-administrators"></a>Administradores do Analysis Services  
 Os administradores [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] podem usar o AMO para automatizar o processamento de bancos de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)]. Por criar e implantar bancos de dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], use o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
##### <a name="developers"></a>Desenvolvedores  
 Os desenvolvedores podem usar AMO para desenvolver interfaces administrativas para conjuntos especificados de usuários. Essas interfaces podem restringir acesso a objetos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] e podem limitar os usuários a certas tarefas. Por exemplo, usando o AMO, é possível criar um aplicativo Backup para permitir que um usuário veja todos os objetos de banco de dados, selecione qualquer um dos bancos de dados e faça backup em qualquer conjunto de dispositivos especificado.  
  
 Os desenvolvedores também podem inserir a lógica do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] em seus aplicativos. Para isso, eles podem criar cubos, dimensões, estruturas de mineração e modelos de mineração baseados em entradas de usuário ou em outros fatores.  
  
##### <a name="olap-advanced-users"></a>Usuários avançados de OLAP  
 Normalmente, os usuários avançados de OLAP são analistas de dados e outros usuários de dados experientes com muitos conhecimentos em programação e que desejam aprimorar suas análises de dados por meio do uso mais próximo dos objetos de dados. Para usuários que tenham de trabalhar offline, o AMO pode ser muito útil na automação da criação de cubos locais antes da entrada no modo offline.  
  
##### <a name="data-mining-advanced-users"></a>Usuários avançados de mineração de dados  
 Para usuários avançados de mineração de dados, o AMO será muito útil se você tiver grandes conjuntos de modelos que devam ser periodicamente treinados outra vez.  
  
##  <a name="AutomatingAdministrativeTaskswithAMO"></a> Automatizando tarefas administrativas com AMO  
 A maioria das tarefas repetitivas será melhor criada, implantada e mantida se for desenvolvida usando o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] em vez de ser desenvolvida como um aplicativo em qualquer linguagem de sua escolha. No entanto, para as tarefas repetitivas que não puderem ser automatizadas com o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)], é possível usar o AMO. O AMO também será útil para quando você quiser desenvolver um aplicativo especializado para business intelligence usando o [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)].  
  
##### <a name="automatic-object-management"></a>Gerenciamento automático de objetos  
 Com o AMO, é muito fácil criar, atualizar ou excluir objetos do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)] (por exemplo, <xref:Microsoft.AnalysisServices.Database>, <xref:Microsoft.AnalysisServices.Dimension>, <xref:Microsoft.AnalysisServices.Cube>, <xref:Microsoft.AnalysisServices.MiningStructure> de mineração e <xref:Microsoft.AnalysisServices.MiningModel> ou <xref:Microsoft.AnalysisServices.Role>) com base na entrada de usuário ou em dados novos obtidos. O AMO é ideal para aplicativos de instalação que precisam implantar uma solução desenvolvida, de um fornecedor de software independente para um cliente final. O aplicativo de instalação pode verificar a existência de uma versão anterior e pode atualizar a estrutura, remover objetos que não são mais úteis e criar novos. Se não houver uma versão anterior, será possível criar tudo do zero.  
  
 O AMO pode ser poderoso para a criação de novas partições baseadas em dados novos e pode remover partições antigas que tenham ido além do escopo do projeto. Por exemplo, para uma solução de análise financeira que trabalha com os últimos 36 meses de dados, assim que um novo mês de dados for recebido, o 37o mês mais antigo poderia ser removido. Para otimizar desempenho, novas agregações podem ser criadas com base em utilização e aplicadas aos últimos 12 meses.  
  
##### <a name="automatic-object-processing"></a>Processamento automático de objetos  
 O processamento de objetos e a disponibilidade atualizada podem ser obtidos ao fazermos com que o AMO responda a certos eventos além do fluxo de dados comum e das tarefas agendadas que utilizam o [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)].  
  
##### <a name="automatic-security-management"></a>Gerenciamento automático de segurança  
 O gerenciamento de segurança pode ser automatizado para incluir novos usuários em funções e permissões ou para remover outros usuários assim que seu tempo tenha expirado. Novas interfaces podem ser criadas para a simplificação do gerenciamento de segurança para administradores de segurança. Isso pode ser mais simples do que usar o [!INCLUDE[ssBIDevStudioFull](../../../includes/ssbidevstudiofull-md.md)].  
  
##### <a name="automatic-backup-management"></a>Gerenciamento automático de backup  
 O gerenciamento automático de backup pode ser feito por meio de tarefas do [!INCLUDE[ssISnoversion](../../../includes/ssisnoversion-md.md)] ou pela criação de aplicativos AMO especializados com execução automática. Usando o AMO, você pode desenvolver interfaces de Backup para operadores e assim ajudá-los em suas tarefas diárias.  
  
##### <a name="tasks-amo-is-not-intended-for"></a>Tarefas para as quais o AMO não foi planejado  
 O AMO não pode ser usado para consultar dados. Para consultar dados do [!INCLUDE[ssASnoversion](../../../includes/ssasnoversion-md.md)], incluindo cubos e modelos de mineração, use o ADOMD.NET a partir de um aplicativo do usuário. Para obter mais informações, consulte [desenvolvendo com ADOMD.NET](../../../analysis-services/multidimensional-models/adomd-net/developing-with-adomd-net.md).  
  
  
