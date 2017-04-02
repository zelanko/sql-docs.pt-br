---
title: "Li&#231;&#227;o 14: Implantar | Microsoft Docs"
ms.custom: ""
ms.date: "02/27/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
ms.tgt_pltfrm: ""
ms.topic: "get-started-article"
applies_to: 
  - "SQL Server 2016"
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 25
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
---
# Li&#231;&#227;o 14: Implantar
Nesta lição, você configurará propriedades de implantação; especificando uma instância de servidor de implantação do Analysis Services executada no modo de Tabela e um nome para o modelo que você está implantando. Você implantará o modelo nessa instância. Depois de implantado, os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório. Para saber mais, consulte [Implantação de uma solução de modelo de tabela &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## Pré-requisitos  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 13: Analisar no Excel](../analysis-services/lesson-13-analyze-in-excel.md).  
  
## Implantar o modelo  
  
#### Para configurar propriedades de implantação  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Modelo de Tabela de Vendas pela Internet do Adventure Works** e, no menu de contexto, clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Páginas de Propriedades de Modelo de Tabela de Vendas pela Internet do AW**, em **Servidor de Implantação**, na propriedade **Server**, digite o nome de uma instância do Analysis Services executada no modo de Tabela. Esta será a instância na qual seu modelo será implantado.  
  
    > [!IMPORTANT]  
    > Você deve ter permissões de Administrador em uma instância do Analysis Services para implantá-la.  
  
3.  Na propriedade **Database**, digite **Modelo de Vendas pela Internet do Adventure Works**.  
  
4.  Na propriedade **Cube Name**, digite **Modelo de Vendas pela Internet do Adventure Works**.  
  
5.  Verifique as seleções e clique em **OK**.  
  
#### Para implantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Criar** e em **Implantar Modelo de Tabela de Vendas pela Internet do AW**.  
  
    A caixa de diálogo Implantar aparecerá com o status de implantação dos metadados e cada tabela incluída no modelo.  
  
2. Quando a implantação for concluída com êxito, continue e clique em **Fechar**.  
  
## Conclusão  
Parabéns! Você concluiu a criação e implantação de seu primeiro modelo de Tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório como o Microsoft Excel ou o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## Recursos adicionais  
Para saber mais sobre as propriedades do modelo de tabela que dão suporte aos relatórios do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], consulte [Propriedades de relatório do Power View &#40;SSAS Tabular&#41;](../analysis-services/tabular-models/power-view-reporting-properties-ssas-tabular.md).  
  
## Consulte também  
[Modo DirectQuery &#40;SSAS de tabela&#41;](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[Configurar propriedades padrão de implantação e modelagem de dados &#40;SSAS de Tabela&#41;](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[Bancos de dados de modelo de tabela &#40;SSAS de Tabela&#41;](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  
