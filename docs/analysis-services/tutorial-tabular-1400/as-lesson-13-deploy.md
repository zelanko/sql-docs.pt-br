---
title: 'Lição do Analysis Services tutorial 13: implantar | Microsoft Docs'
ms.date: 05/08/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 57ddfe2f2d00b098fbffa40811a7877752fefed4
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="deploy"></a>Implantar

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você configurar propriedades de implantação. especificar um servidor para implantar e um nome para o modelo. Implantar o modelo para o servidor. Depois que o modelo é implantado, os usuários podem se conectar a ele usando um aplicativo cliente de relatório. Para obter mais informações, consulte [implantar no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) e [implantação de solução de modelo de tabela](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 12: analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Se implantar serviços de análise do Azure, você deve ter [permissões de administrador](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) sobre o serever.  

> [!IMPORTANT]  
> Se você instalou o banco de dados de exemplo AdventureWorksDW em um SQL Server local e você estiver implantando seu modelo em um servidor de serviços de análise do Azure, uma [gateway de dados no local](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) é necessária.
  
## <a name="deploy-the-model"></a>Implantar o modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propriedades de implantação  

  
1.  Em **Solution Explorer**, com o botão direito do **de vendas pela Internet AW** do projeto e, em seguida, clique em **propriedades**.  
  
2.  No **páginas de propriedades de vendas de Internet AW** caixa de diálogo **servidor de implantação**, no **Server** propriedade, digite o nome de servidor completo. Se estiver se conectando ao Azure Analysis Services, o nome do servidor deve incluem a URL completa.

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  No **banco de dados** propriedade, digite **Adventure Works Internet Sales**.  
  
4.  No **nome do modelo** propriedade, digite **modelo de vendas do Adventure Works Internet**.  
  
5.  Verifique as seleções e clique em **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Para implantar Adventure Works Internet Sales
  
1.  Em **Solution Explorer**, com o botão direito do **de vendas pela Internet AW** projeto > **criar**.  

2.  Clique com botão direito do **de vendas pela Internet AW** projeto > **implantar**.

    Ao implantar serviços de análise do Azure, você pode ser solicitado a inserir sua conta. Insira sua conta organizacional e senha, por exemplo nancy@adventureworks.com. Essa conta deve estar em Administradores no servidor.
  
    A caixa de diálogo implantar aparece e exibe o status da implantação de metadados e cada tabela incluído no modelo.  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Quando a implantação for concluída com êxito, continue e clique em **Fechar**.  
  

Esta lição descreve o método mais fácil e mais comuns para implantar um modelo de tabela do SSDT. Opções de implantação avançada, como o Assistente de implantação ou automatizar com XMLA e AMO fornecem maior flexibilidade, consistência e implantações agendadas. Para obter mais informações, consulte [implantação de solução de modelo de tabela](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Conclusão  
Parabéns! Você terminar de criar e implantar seu primeiro modelo de tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários agora também podem se conectar ao modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou Power BI.  

![ssms como lesson13](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>O que vem a seguir?
[Conecte-se com o Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Lição suplementar - segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Lição suplementar - linhas de detalhes](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Lição suplementar - hierarquias desbalanceadas](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
