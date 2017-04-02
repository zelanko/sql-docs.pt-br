---
title: "Li&#231;&#227;o 1: Criar um novo projeto de modelo de tabela | Microsoft Docs"
ms.custom: ""
ms.date: "03/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
caps.latest.revision: 33
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 28
---
# Li&#231;&#227;o 1: Criar um novo projeto de modelo de tabela
Nesta lição, você criará um novo projeto de modelo de tabela em branco no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Quando seu novo projeto é criado, você pode começar a adicionar dados usando o Assistente de Importação de Tabela. Além de criar um novo projeto, esta lição inclui também uma introdução breve ao ambiente de criação de modelo de tabela em [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
Para saber mais sobre os diferentes tipos de projetos de modelo de tabela, consulte [Projetos de modelo de tabela &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/tabular-model-projects-ssas-tabular.md). Para saber mais sobre o ambiente de criação do modelo de tabela, consulte [Designer de modelo de tabela &#40;SSAS&#41;](../analysis-services/tabular-models/tabular-model-designer-ssas.md).  
  
Tempo estimado para concluir esta lição: **10 minutos**  
  
## Pré-requisitos  
Este tópico é a primeira lição em um tutorial de criação de modelo de tabela. Para concluir esta lição, você deve ter o banco de dados AdventureWorksDW instalado em uma instância do SQL Server. Para obter mais informações, consulte [Modelagem de tabela &#40;Tutorial do Adventure Works&#41;](../analysis-services/tabular-modeling-adventure-works-tutorial.md).  
  
## Criar um novo projeto de modelo de tabela  
  
#### Para criar um novo projeto de modelo de tabela  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  Na caixa de diálogo **Novo Projeto**, em **Instalado**, clique em **Business Intelligence**, em **Analysis Services** e em **Projeto de Tabela do Analysis Services**.  
  
3.  Em **Nome**, digite **Modelo de Tabela de Vendas pela Internet do AW** e especifique um local para os arquivos de projeto.  
  
    Por padrão, o **Nome da Solução** será igual ao nome do projeto; no entanto, você poderá digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
5.  Na caixa de diálogo **Designer de modelo de tabela**, em **Servidor de espaço de trabalho**, digite o nome de uma instância do SQL Server 2016 Analysis Services em que você tem permissões de Administrador do Servidor e clique em **Testar Conexão**.  
  
    A instância de servidor do Espaço de Trabalho que você especificar hospedará um modelo de banco de dados de Tabela com o mesmo nome do projeto durante a criação.   
      
6.  Em **Nível de compatibilidade**, verifique se a opção **SQL Server 2016 (1200)** está selecionada e clique em **OK**.   
      
    Se SQL Server 2016 (1200) não está visível na caixa de listagem Nível de compatibilidade, isso significa que você não está usando a versão mais recente do SQL Server Data Tools. Para obter a versão mais recente, consulte [Instalar o SQL Server Data Tools](https://msdn.microsoft.com/hh500335(v=vs.103).aspx).   
      
    É recomendado selecionar um nível de compatibilidade anterior somente se você pretende implantar o modelo de Tabela concluído em uma instância do Analysis Services diferente que executa o SQL Server 2012 ou 2014. Para saber mais, consulte [Nível de compatibilidade](../analysis-services/tabular-models/compatibility-level-for-tabular-models-in-analysis-services.md).   
  
## Compreendendo o ambiente de criação do modelo de tabela de ferramentas de dados do SQL Server  
Agora que você criou um novo projeto de modelo tabular, vamos dedicar um tempo para explorar o ambiente de criação de modelo tabular no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 ou posterior).  
  
Depois que seu projeto for criado, ele será aberto no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Um modelo vazio será exibido no designer de modelos e o arquivo **Model.bim** estará selecionado na janela **Gerenciador de Soluções**. Quando você adiciona dados, tabelas e colunas aparecerão no designer. Se o designer não estiver visível (a janela vazia com a guia Model.bim), em **Gerenciador de Soluções**, em **Modelo de Tabela de Vendas pela Internet do AW**, clique duas vezes no arquivo **Model.bim**.  
  
Você pode exibir as propriedades básicas de projeto na janela **Propriedades**. Em **Gerenciador de Soluções**, clique em **Modelo de Tabela de Vendas pela Internet do AW**. Observe que, na janela **Propriedades**, em **Arquivo de Projeto**, você verá **Modelo de Tabela de Vendas pela Internet do AW.smproj**. Esse é o nome do arquivo de projeto e, em **Pasta do Projeto**, você verá o local do arquivo do projeto.  
  
No **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Modelo de Tabela de Vendas pela Internet do AW** e clique em **Propriedades**. A caixa de diálogo **Páginas de Propriedades de Modelo de Tabela de Vendas pela Internet do AW** é exibida. Essas são as propriedades de projeto avançadas. Você definirá posteriormente algumas dessas propriedades quando estiver pronto para implantar o modelo.  
  
Agora, vamos analisar as propriedades do modelo. Em **Gerenciador de Soluções**, clique em **Model.bim**. Na janela **Propriedades**, você verá as propriedades do modelo, sendo **Modo DirectQuery** a mais importante delas. Essa propriedade especifica se o modelo será implantado ou não no modo Na Memória (Desativado) ou no modo DirectQuery (Ativado). Neste tutorial, você criará e implantará o modelo no modo Em Memória.  
  
Quando você criar um novo modelo, determinadas propriedades de modelo serão definidas automaticamente de acordo com as configurações de Modelagem de Dados que podem ser especificadas na caixa de diálogo de Ferramentas\Opções. As propriedades de Backup de Dados, Retenção de Espaço de trabalho e Servidor de Espaço de Trabalho especificam como e onde o banco de dados de espaço de trabalho (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você poderá alterar essas configurações posteriormente se necessário, mas, por enquanto, deixe essas propriedades como estão.  
  
Quando você instalar o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], vários novos itens de menu serão adicionados ao ambiente do Visual Studio. Vamos analisar os novos itens de menu que são específicos da criação dos modelos de tabela. Clique no menu **Modelo**. Aqui, você pode iniciar o Assistente de Importação de Tabela, exibir e editar conexões existentes, atualizar dados do espaço de trabalho, procurar seu modelo no [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel com o recurso Analisar no Excel, criar perspectivas e funções, selecionar a exibição do modelo e definir opções de cálculo.  
  
Clique no menu **Tabela**. Aqui, você pode criar e gerenciar relações entre tabelas, criar e gerenciar, especifique configurações de tabela de data, criar partições e editar propriedades de tabela.  
  
Clique no menu **Coluna**. Aqui, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. Você também pode usar o recurso AutoSum para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Embora alguns itens ainda não estejam ativos, você poderá ter uma boa noção do ambiente de criação de modelo de tabela.  
  
## Próximas etapas  
Para continuar este tutorial, vá para a próxima lição: [Lição 2: Adicionar dados](../analysis-services/lesson-2-add-data.md).  
  
  
  
