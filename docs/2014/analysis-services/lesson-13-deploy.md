---
title: 'Lição 14: implantar | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: 96ffa6445d46f1e68efa907330d0945a499bf3b2
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66079139"
---
# <a name="lesson-14-deploy"></a>Lição 14: Implantar
  Nesta lição, você configurará propriedades de implantação; especificando uma instância de servidor de implantação do Analysis Services executada no modo de Tabela e um nome para o modelo que você está implantando. Você implantará o modelo nessa instância. Depois de implantado, os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório. Para saber mais, consulte [Implantação de uma solução de modelo de tabela &#40;SSAS Tabular&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 13: Analisar no Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implantar o modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propriedades de implantação  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Modelo de Tabela de Vendas pela Internet do Adventure Works** e, no menu de contexto, clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Páginas de Propriedades de Modelo de Tabela de Vendas pela Internet do AW** , em **Servidor de Implantação**, na propriedade **Server** , digite o nome de uma instância do Analysis Services executada no modo de Tabela. Esta será a instância na qual seu modelo será implantado.  
  
    > [!IMPORTANT]  
    >  Você deve ter permissões de Administrador em uma instância do Analysis Services para implantá-la.  
  
3.  Verifique se a propriedade **modo de consulta** está definida como **na memória**.  
  
    > [!NOTE]  
    >  Não há suporte para o modelo criado por meio deste tutorial no modo DirectQuery.  
  
4.  Na propriedade de **banco** de dados `Adventure Works Internet Sales Model`, digite.  
  
5.  Na propriedade nome do **cubo** , digite `Adventure Works Internet Sales Model`.  
  
6.  Verifique suas seleções e então clique em **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Criar** e em **Implantar Modelo de Tabela de Vendas pela Internet do AW**.  
  
     A caixa de diálogo Implantar aparecerá com o status de implantação dos metadados e cada tabela incluída no modelo.  
  
## <a name="conclusion"></a>Conclusão  
 Parabéns! Você é terminou de criar e implantar seu primeiro modelo de tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório como o Microsoft Excel ou o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Recursos adicionais  
 Para saber mais sobre as propriedades do modelo de tabela que dão suporte aos relatórios do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], consulte [Propriedades de relatório do Power View &#40;SSAS Tabular&#41;](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar propriedades de implantação e modelagem de dados padrão &#40;SSAS tabular&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Bancos de dados de modelo de tabela &#40;SSAS de Tabela&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
