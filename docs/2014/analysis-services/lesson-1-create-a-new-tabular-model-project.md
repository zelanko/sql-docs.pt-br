---
title: 'Lição 1: Criar um novo projeto de modelo de tabela | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- analysis-services
ms.topic: conceptual
ms.assetid: 0d2eb34d-78c8-41ff-b92d-49b62c16b2ac
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 7d7ab0a864d99e3cade96b7715adf7d307ca355c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62729463"
---
# <a name="lesson-1-create-a-new-tabular-model-project"></a>Lição 1: Criar um novo projeto de modelo de tabela
  Nesta lição, você criará um novo projeto de modelo de tabela em branco no [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)]. Quando seu novo projeto é criado, você pode começar a adicionar dados usando o Assistente de Importação de Tabela. Além de criar um novo projeto, esta lição inclui também uma introdução breve ao ambiente de criação de modelo de tabela em [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)].  
  
 Para saber mais sobre os diferentes tipos de projetos de modelo de tabela, consulte [Projetos de modelo de tabela &#40;SSAS Tabular&#41;](tabular-models/tabular-model-projects-ssas-tabular.md). Para saber mais sobre o ambiente de criação de modelos tabulares, consulte [Designer de modelo de tabela &#40;SSAS de tabela&#41;](tabular-model-designer-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **10 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico é a primeira lição em um tutorial de criação de modelo de tabela. Para concluir esta lição, você deve ter o banco de dados AdventureWorksDW instalado em uma instância do SQL Server. Para obter mais informações, consulte [Modelagem de tabela &#40;Tutorial do Adventure Works&#41;](tabular-modeling-adventure-works-tutorial.md).  
  
## <a name="create-a-new-tabular-model-project"></a>Criar um novo projeto de modelo de tabela  
  
#### <a name="to-create-a-new-tabular-model-project"></a>Para criar um novo projeto de modelo de tabela  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no menu **Arquivo** , clique em **Novo**e, em seguida, em **Projeto**.  
  
2.  No **novo projeto** caixa de diálogo **modelos instalados**, clique em **Business Intelligence**, em seguida, clique em **Analysis Services**, e em seguida, clique em **projeto Tabular do Analysis Services**.  
  
3.  Na **nome**, digite `AW Internet Sales Tabular Model`, em seguida, especifique um local para os arquivos de projeto.  
  
     Por padrão, o **Nome da Solução** será igual ao nome do projeto; no entanto, você poderá digitar outro nome de solução.  
  
4.  Clique em **OK**.  
  
## <a name="understanding-the-sql-server-data-tools-tabular-model-authoring-environment"></a>Compreendendo o ambiente de criação do modelo de tabela de ferramentas de dados do SQL Server  
 Agora que você criou um novo projeto de modelo de tabela, vamos dedicar um tempo para explorar o ambiente de criação de modelos tabulares [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] (Visual Studio 2010 ou posterior).  
  
 Depois que seu projeto for criado, ele será aberto no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)]. Um modelo vazio será exibido no designer de modelos e o arquivo **Model.bim** estará selecionado na janela **Gerenciador de Soluções** . Quando você adiciona dados, tabelas e colunas aparecerão no designer. Se você não vir o designer (a janela vazia com a guia Model. BIM), em **Gerenciador de soluções**, em `AW Internet Sales Tabular Model`, clique duas vezes o **Model. BIM** arquivo.  
  
 Você pode exibir as propriedades básicas de projeto na janela **Propriedades** . Na **Gerenciador de soluções**, clique em `AW Internet Sales Tabular Model`. Observe que, na janela **Propriedades** , em **Arquivo de Projeto**, você verá **Modelo de Tabela de Vendas pela Internet do AW.smproj**. Esse é o nome do arquivo de projeto e, em **Pasta do Projeto**, você verá o local do arquivo do projeto.  
  
 No **Gerenciador de soluções**, clique com botão direito do `AW Internet Sales Tabular Model` de projeto e, em seguida, clique em **propriedades**. A caixa de diálogo **Páginas de Propriedades de Modelo de Tabela de Vendas pela Internet do AW** é exibida. Essas são as propriedades de projeto avançadas. Você definirá posteriormente algumas dessas propriedades quando estiver pronto para implantar o modelo.  
  
 Agora, vamos examinar as propriedades do modelo. Em **Gerenciador de Soluções**, clique em **Model.bim**. Na janela **Propriedades** , você verá as propriedades do modelo, sendo **Modo DirectQuery** a mais importante delas. Essa propriedade especifica se o modelo será implantado ou não no modo Na Memória (Desativado) ou no modo DirectQuery (Ativado). Neste tutorial, você criará e implantará o modelo no modo Em Memória.  
  
 Quando você criar um novo modelo, determinadas propriedades de modelo serão definidas automaticamente de acordo com as configurações de Modelagem de Dados que podem ser especificadas na caixa de diálogo de Ferramentas\Opções. As propriedades de Backup de Dados, Retenção de Workspace e Servidor de Workspace especificam como e onde o banco de dados de workspace (seu banco de dados de criação de modelo) será submetido a backup, retido na memória e compilado. Você poderá alterar essas configurações posteriormente se necessário, mas, por enquanto, deixe essas propriedades como estão.  
  
 Quando você instalar o [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], vários novos itens de menu serão adicionados ao ambiente do Visual Studio. Vamos examinar os novos itens de menu que são específicos para a criação de modelos de tabela. Clique no menu **Modelo** . Aqui, você pode iniciar o Assistente de Importação de Tabela, exibir e editar conexões existentes, atualizar dados do workspace, procurar seu modelo no [!INCLUDE[msCoName](../includes/msconame-md.md)] Excel com o recurso Analisar no Excel, criar perspectivas e funções, selecionar a exibição do modelo e definir opções de cálculo.  
  
 Clique no menu **Tabela**. Aqui, você pode criar e gerenciar relações entre tabelas, criar e gerenciar, especifique configurações de tabela de data, criar partições e editar propriedades de tabela.  
  
 Clique no menu **Coluna** . Aqui, você pode adicionar e excluir colunas em uma tabela, congelar colunas e especificar a ordem de classificação. Você também pode usar o recurso AutoSum para criar uma medida de agregação padrão para uma coluna selecionada. Outros botões da barra de ferramentas fornecem acesso rápido a recursos e comandos frequentemente usados.  
  
 Explore algumas das caixas de diálogo e locais de vários recursos específicos da criação de modelos de tabela. Embora alguns itens ainda não estejam ativos, você poderá ter uma boa noção do ambiente de criação de modelo de tabela.  
  
## <a name="next-steps"></a>Próximas etapas  
 Para continuar este tutorial, vá para a próxima lição: [Lição 2: Adicionar dados](lesson-2-add-data.md).  
  
  
