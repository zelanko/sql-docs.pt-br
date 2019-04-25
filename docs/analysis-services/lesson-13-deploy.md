---
title: 'Lição 13: Implantar | Microsoft Docs'
ms.date: 08/22/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 6b2ed8149cef9e9886398feebf43329f962b9537
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62467603"
---
# <a name="lesson-13-deploy"></a>Lição 13: Implantar
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição, você irá configurar as propriedades de implantação especificando um local ou instância de servidor do Azure e um nome para o modelo. Em seguida, você implantará o modelo a essa instância. Depois que o modelo é implantado, os usuários podem se conectar a ele por meio de um aplicativo cliente de relatório. Para saber mais sobre a implantação, consulte [implantação de solução de modelo Tabular](../analysis-services/tabular-models/tabular-model-solution-deployment-ssas-tabular.md) e [implantar no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  
Este tópico faz parte de um tutorial de modelo de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [Lição 12: Analisar no Excel](../analysis-services/lesson-12-analyze-in-excel.md).  
  
## <a name="deploy-the-model"></a>Implantar o modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propriedades de implantação  
  
1.  No **Gerenciador de soluções**, clique com botão direito do **vendas pela Internet AW** de projeto e, em seguida, clique em **propriedades**.  
  
2.  No **páginas de propriedades de vendas de Internet do AW** caixa de diálogo **servidor de implantação**, no **Server** propriedade, digite o nome de um servidor do Azure Analysis Services ou um instância de servidor local executando no modo de tabela. Essa será a instância do servidor que será implantado em seu modelo.  

    ![aas-deploy-deployment-server-property](../analysis-services/media/aas-deploy-deployment-server-property.png)
 
    > [!IMPORTANT]  
    > Você deve ter permissões de administrador no remoto do Analysis Services instância para poder implantá-la.  
  
3.  No **banco de dados** propriedade, digite **Adventure Works Internet Sales**.  
  
4.  No **nome do modelo** propriedade, digite **modelo do Adventure Works Internet Sales**.  
  
5.  Verifique as seleções e clique em **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales-tabular-model"></a>Para implantar o modelo de tabela de vendas pela Internet da Adventure Works.  
  
1.  No **Gerenciador de soluções**, clique com botão direito do **vendas pela Internet AW** projeto > **compilar**.  

2.  Clique com botão direito do **vendas pela Internet AW** projeto > **implantar**.

    Ao implantar o Azure Analysis Services, você provavelmente será solicitado a inserir sua conta. Insira sua conta organizacional e senha, por exemplo nancy@adventureworks.com. Essa conta deve constar na lista Admins na instância do servidor.
  
    A caixa de diálogo Implantar aparecerá com o status de implantação dos metadados e cada tabela incluída no modelo.  
    
    ![aas-deploy-status](../analysis-services/media/aas-deploy-status.png)
  
3. Quando a implantação for concluída com êxito, continue e clique em **Fechar**.  
  
## <a name="conclusion"></a>Conclusão  
Parabéns! Você terminou a criar e implantar seu primeiro modelo de tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários agora também podem se conectar ao modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou Power BI.  

![as-tabular-lesson13-ssms](../analysis-services/media/as-tabular-lesson13-ssms.png)
  
  
## <a name="see-also"></a>Confira também  
[Modo DirectQuery](../analysis-services/tabular-models/directquery-mode-ssas-tabular.md)  
[Configurar propriedades de implantação e modelagem de dados padrão](../analysis-services/tabular-models/configure-default-data-modeling-and-deployment-properties-ssas-tabular.md)  
[Bancos de dados modelo de tabela](../analysis-services/tabular-models/tabular-model-databases-ssas-tabular.md)  
  
  
  ## <a name="whats-next"></a>O que vem a seguir?
*  [Lição suplementar – implementar a segurança dinâmica usando filtros de linha](../analysis-services/supplemental-lesson-implement-dynamic-security-by-using-row-filters.md).

*  [Complementares lição – configurar propriedades de relatório para relatórios do Power View](../analysis-services/supplemental-lesson-configure-reporting-properties-for-power-view-reports.md).
