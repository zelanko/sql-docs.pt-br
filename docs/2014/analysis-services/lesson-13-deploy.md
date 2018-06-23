---
title: 'Lição 14: Implantar | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 24863a8a-9017-415a-a97b-fbac76ed0675
caps.latest.revision: 19
author: Minewiskan
ms.author: owend
manager: jhubbard
ms.openlocfilehash: 2b9bf4afde77cc0438e097c14f6b3743c7da427d
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117281"
---
# <a name="lesson-14-deploy"></a>Lição 14: Implantar
  Nesta lição, você configurará propriedades de implantação; especificando uma instância de servidor de implantação do Analysis Services executada no modo de Tabela e um nome para o modelo que você está implantando. Você implantará o modelo nessa instância. Depois de implantado, os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório. Para saber mais, consulte [Implantação de uma solução de modelo de tabela &#40;SSAS Tabular&#41;](tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
 Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
 Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição, você deverá ter concluído a lição anterior: [Lição 13: Analisar no Excel](lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implantar o modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propriedades de implantação  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], no **Gerenciador de Soluções**, clique com o botão direito do mouse no projeto **Modelo de Tabela de Vendas pela Internet do Adventure Works** e, no menu de contexto, clique em **Propriedades**.  
  
2.  Na caixa de diálogo **Páginas de Propriedades de Modelo de Tabela de Vendas pela Internet do AW** , em **Servidor de Implantação**, na propriedade **Server** , digite o nome de uma instância do Analysis Services executada no modo de Tabela. Esta será a instância na qual seu modelo será implantado.  
  
    > [!IMPORTANT]  
    >  Você deve ter permissões de Administrador em uma instância do Analysis Services para implantá-la.  
  
3.  Verifique se o **o modo de consulta** está definida como **na memória**.  
  
    > [!NOTE]  
    >  Não há suporte para o modelo criado por meio deste tutorial no modo DirectQuery.  
  
4.  No **banco de dados** propriedade, digite `Adventure Works Internet Sales Model`.  
  
5.  No **cubo** propriedade Name, digite `Adventure Works Internet Sales Model`.  
  
6.  Verifique as seleções e clique em **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Criar** e em **Implantar Modelo de Tabela de Vendas pela Internet do AW**.  
  
     A caixa de diálogo Implantar aparecerá com o status de implantação dos metadados e cada tabela incluída no modelo.  
  
## <a name="conclusion"></a>Conclusão  
 Parabéns! Você é terminou de criar e implantar seu primeiro modelo de tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários podem se conectar ao modelo usando um aplicativo cliente de relatório como o Microsoft Excel ou o [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)].  
  
## <a name="additional-resources"></a>Recursos adicionais  
 Para saber mais sobre as propriedades do modelo de tabela que dão suporte aos relatórios do [!INCLUDE[ssCrescent](../includes/sscrescent-md.md)], consulte [Propriedades de relatório do Power View &#40;SSAS Tabular&#41;](tabular-models/properties-ssas-tabular.md).  
  
## <a name="see-also"></a>Consulte também  
 [Modo DirectQuery &#40;SSAS de tabela&#41;](tabular-models/directquery-mode-ssas-tabular.md)   
 [Configurar propriedades de implantação e modelagem de dados padrão &#40;Tabular do SSAS&#41;](tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)   
 [Bancos de dados de modelo de tabela &#40;Tabular do SSAS&#41;](tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  