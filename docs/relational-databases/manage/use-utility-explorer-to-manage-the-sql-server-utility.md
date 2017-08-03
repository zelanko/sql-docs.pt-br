---
title: "Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 74012c90-b42e-4171-b27a-9c30cf69ff98
caps.latest.revision: 10
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: bd65300d9d3c79ea0604d6ea83c1c9377b7982cc
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="use-utility-explorer-to-manage-the-sql-server-utility"></a>Usar o Gerenciador do Utilitário para gerenciar o Utilitário do SQL Server
  O Gerenciador do Utilitário, um componente do [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecta-se a instâncias do [!INCLUDE[ssDE](../../includes/ssde-md.md)] para fornecer uma exibição de árvore de todos os objetos no Utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . O painel de conteúdo do Gerenciador do Utilitário oferece várias formas de exibir dados resumidos e detalhados sobre o estado de integridade de instâncias gerenciadas do SQL Server. O Gerenciador do Utilitário também oferece uma interface do usuário para exibir e gerenciar definições de políticas. Os recursos de Gerenciador do Utilitário variam ligeiramente, dependendo dos objetos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, mas em geral incluem objetos, dados e políticas gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md).  
  
## <a name="create-utility-control-point"></a>Criar ponto de controle do utilitário  
 Para que você possa usar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, deve criar um ponto de controle do utilitário. Para obter mais informações, veja [Recursos e tarefas do Utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md) ou [Criar um ponto de controle do utilitário do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/create-a-sql-server-utility-control-point-sql-server-utility.md).  
  
## <a name="enroll-an-instance-of-sql-server-or-a-data-tier-application-from-utility-explorer"></a>Inscrever uma instância do SQL Server ou um aplicativo da camada de dados no Gerenciador do Utilitário  
 Você pode facilmente inscrever uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. No Gerenciador do Utilitário, clique com o botão direito do mouse no nó **Instâncias Gerenciadas** e clique em **Adicionar Instância Gerenciada**. Siga as etapas do assistente para concluir a operação. Para obter mais informações, veja [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md).  
  
 Para implantar um aplicativo da camada de dados em uma instância gerenciada do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], clique na guia **Pesquisador de Objetos**, expanda o nó **Gerenciamento** e clique com o botão direito do mouse em **Aplicativos da Camada de Dados**. No menu de atalho, selecione **Implantar Aplicativo da Camada de Dados**. Para obter mais informações, veja [Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md).  
  
## <a name="viewing-utility-explorer"></a>Exibindo o Gerenciador do Utilitário  
 O Gerenciador do Utilitário não fica visível no [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] por padrão. Se você não puder ver o Gerenciador do Utilitário na interface do usuário do [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] , no menu **Exibir** , clique em **Gerenciador do Utilitário**. Para exibir o painel de conteúdo do Gerenciador do Utilitário, no menu **Exibir** , clique em **Conteúdo do Gerenciador do Utilitário**.  
  
## <a name="viewing-objects-in-utility-explorer"></a>Exibindo objetos no Gerenciador do Utilitário  
 O painel de navegação do Gerenciador do Utilitário e o painel de conteúdo do Gerenciador do Utilitário exibem dados, objetos e políticas gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Use o painel de navegação para especificar as informações a serem exibidas no painel e nos pontos de vista. Em seguida, use o painel de conteúdo e as guias de detalhes para acessar dados e informações sobre políticas para objetos gerenciados pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility.  
  
### <a name="sql-server-utility-navigation-pane"></a>Painel de navegação do Utilitário do SQL Server  
 O painel de navegação do Gerenciador do Utilitário oferece uma exibição de árvore de objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, agrupados por ponto de controle do utilitário. Para expandir pastas, clique no sinal de adição (+) ou clique duas vezes no nome do UCP no painel de navegação do Gerenciador do Utilitário. Clique com o botão direito do mouse em pastas ou objetos para executar tarefas comuns. Os nós na exibição de árvore são como se segue:  
  
-   O nó superior na exibição de árvore é o UCP (ponto de controle do utilitário). O nome do nó é construído da seguinte maneira: "Nome_do_Utilitário" (NomeDoComputador\nome_da_instância_UCP). Se você não tiver um UCP, deverá criar um. Se você não estiver conectado a um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility, deverá conectar-se a um. Para obter mais informações, consulte [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md). Clique no nome do UCP na exibição de árvore para popular o painel de conteúdo do Gerenciador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility com dados na exibição de painel. Para obter mais informações, veja [Painel do Utilitário &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1).  
  
     Clique com o botão direito do mouse no nó UCP para atualizar dados no painel.  
  
-   Clique no nó **Aplicativos da Camada de Dados Implantados** no modo de exibição de árvore para acessar dados da exibição de lista no painel de conteúdo do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As guias de detalhes na parte inferior do painel de conteúdo fornecem dados para utilização de CPU e armazenamento, além de acesso a definições de políticas e detalhes de propriedades para aplicativos da camada de dados individuais no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. Para obter mais informações, veja [Detalhes do aplicativo da camada de dados implantado &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/79c41dd9-abcb-434e-9326-00a341d5c867).  
  
     Clique com o botão direito do mouse no nó **Aplicativos da Camada de Dados Implantados**, no modo de exibição de árvore, para acessar configurações de filtro ou atualizar dados na exibição de lista.  
  
-   Clique no nó **Instâncias Gerenciadas** na exibição de árvore para acessar dados da exibição de lista no painel de conteúdo do Gerenciador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Utility. As guias de detalhes na parte inferior do painel de conteúdo fornecem dados para utilização de CPU e volume de armazenamento, além de acesso a definições de políticas e detalhes de propriedades para instâncias individuais gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no Utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter mais informações, veja [Detalhes de instâncias gerenciadas &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/6e51b7bb-a733-4852-8c33-7f4dbdf931c2).  
  
     Clique com o botão direito do mouse no nó **Instâncias Gerenciadas** no modo de exibição de árvore para adicionar instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ao Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para acessar configurações de filtro ou atualizar dados na exibição de lista.  
  
-   Clique no nó **Administração do Utilitário** do modo de exibição de árvore para acessar definições de políticas globais para todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados implantados no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], para exibir informações de administrador do UCP e para acessar parâmetros de configuração do data warehouse de gerenciamento do Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Administração do Utilitário &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/3e5a00c3-8905-40f0-9ddc-d924df9c2f0d). Você também pode usar controles da guia **Política** para alterar a sensibilidade de relatório de violações de políticas. Para obter mais informações, veja [Reduzir o ruído em políticas de utilização da CPU &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/reduce-noise-in-cpu-utilization-policies-sql-server-utility.md).  
  
     Clique com o botão direito do mouse no nó **Administração do Utilitário** no modo de exibição de árvore para atualizar dados no painel de conteúdo.  
  
### <a name="sql-server-utility-dashboard"></a>Painel do Utilitário do SQL Server  
 A seleção do nó UCP na exibição de árvore do Gerenciador do Utilitário popula o painel do Utilitário [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no painel de conteúdo do Gerenciador do Utilitário. O painel exibe um resumo de status para todas as instâncias gerenciadas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e aplicativos da camada de dados no Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], bem como a utilização de armazenamento global para objetos gerenciados pelo Utilitário do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Painel do Utilitário &#40;Utilitário do SQL Server&#41;](http://msdn.microsoft.com/library/999eb741-4a60-43f6-ab37-2df7dce845c1). Para inscrever ou remover uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Inscrever uma instância do SQL Server &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/enroll-an-instance-of-sql-server-sql-server-utility.md), [Implantar um aplicativo da camada de dados](../../relational-databases/data-tier-applications/deploy-a-data-tier-application.md) ou [Remover uma instância do SQL Server do Utilitário do SQL Server](../../relational-databases/manage/remove-an-instance-of-sql-server-from-the-sql-server-utility.md).  
  
### <a name="filtering-the-list-of-objects-in-utility-explorer-contents"></a>Filtrando a lista de objetos no conteúdo do Gerenciador do Utilitário  
 Quando um nó contém um grande número de objetos, pode ser difícil encontrar o objeto que você está procurando. Nesses casos, use o recurso de filtro do Gerenciador do Utilitário para reduzir a lista para um tamanho menor. Por exemplo, quando você quer localizar uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou somente os computadores com espaço de arquivo subutilizado. Clique com o botão direito do mouse na pasta que deseja filtrar, clique no botão de filtro e clique em **Configurações de Filtro** para abrir a caixa de diálogo Configurações de Filtro do Gerenciador do Utilitário. Você pode filtrar a lista por nome, CPU do computador, CPU da instância, espaço para arquivo, espaço no volume, configurações de substituição de políticas ou último horário reportado. As colunas **Operador** e **Valor** fornecem operadores de filtragem adicionais em uma lista suspensa.  
  
### <a name="starting-powershell"></a>Iniciando o PowerShell  
 Você pode iniciar uma sessão do PowerShell clicando com o botão direito do mouse na maioria das pastas e dos objetos na árvore do Pesquisador de Objetos e selecionando **Iniciar PowerShell**. Isso inicia uma sessão do Powershell que tem o suporte para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Powershell habilitado e o caminho definido até o objeto quando você clicou com o botão direito do mouse no Pesquisador de Objetos. Você pode inserir comandos do Powershell em um ambiente interativo do Powershell. Para saber mais, confira [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md).  
  
 O PowerShell não tem a ajuda F1, mas inclui um cmdlet **Get-Help** que fornece informações sobre como usá-lo. Para obter mais informações sobre como usar Get-Help, veja [Get Help SQL Server PowerShell](../../relational-databases/scripting/get-help-sql-server-powershell.md).  
  
## <a name="see-also"></a>Consulte também  
 [Recursos e tarefas do utilitário do SQL Server](../../relational-databases/manage/sql-server-utility-features-and-tasks.md)   
 [Configurar políticas de integridade &#40;Utilitário do SQL Server&#41;](../../relational-databases/manage/configure-health-policies-sql-server-utility.md)   
 [Pesquisador de Objetos](http://msdn.microsoft.com/library/469ea8e2-79b9-44c8-bb6f-f0e1c5dbf0f2)  
  
  
