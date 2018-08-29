---
title: 'Lição 13 do tutorial de serviços de análise: implantar | Microsoft Docs'
ms.date: 08/27/2018
ms.prod: sql
ms.technology: analysis-services
ms.custom: tabular-models
ms.topic: tutorial
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: bad6f58800e6a023fe5014462fbe6bbaf76bfe8e
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43090428"
---
# <a name="deploy"></a>Implantar

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Nesta lição, você configura as propriedades de implantação especificando para implantar em um servidor e um nome para o modelo. Em seguida, implantar o modelo para o servidor. Depois que o modelo é implantado, os usuários podem se conectar a ele por meio de um aplicativo cliente de relatório. Para obter mais informações, consulte [implantar no Azure Analysis Services](https://docs.microsoft.com/azure/analysis-services/analysis-services-deploy) e [implantação de solução de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).  
  
Tempo estimado para concluir esta lição: **5 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas nesta lição, você deve ter concluído a lição anterior: [lição 12: analisar no Excel](../tutorial-tabular-1400/as-lesson-12-analyze-in-excel.md).  

> [!IMPORTANT]  
> Se implantar no Azure Analysis Services, você deve ter [permissões de administrador](https://docs.microsoft.com/azure/analysis-services/analysis-services-server-admins) sobre o serever.  

> [!IMPORTANT]  
> Se você instalou o banco de dados AdventureWorksDW em um SQL Server no local, e você está implantando seu modelo para um servidor do Azure Analysis Services, uma [gateway de dados locais](https://docs.microsoft.com/azure/analysis-services/analysis-services-gateway) é necessária.
  
## <a name="deploy-the-model"></a>Implantar o modelo  
  
#### <a name="to-configure-deployment-properties"></a>Para configurar propriedades de implantação  

  
1.  No **Gerenciador de soluções**, clique com botão direito do **vendas pela Internet AW** de projeto e, em seguida, clique em **propriedades**.  
  
2.  No **páginas de propriedades de vendas de Internet do AW** caixa de diálogo **servidor de implantação**, no **Server** propriedade, digite o nome completo do servidor. Se estiver se conectando ao Azure Analysis Services, o nome do servidor deve incluem a URL completa.

    ![as-lesson13-deploy-property](../tutorial-tabular-1400/media/as-lesson13-deploy-property.png)
  
3.  No **banco de dados** propriedade, digite **Adventure Works Internet Sales**.  
  
4.  No **nome do modelo** propriedade, digite **modelo do Adventure Works Internet Sales**.  
  
5.  Verifique as seleções e clique em **OK**.  
  
#### <a name="to-deploy-the-adventure-works-internet-sales"></a>Para implantar a Adventure Works Internet Sales
  
1.  No **Gerenciador de soluções**, clique com botão direito do **vendas pela Internet AW** projeto > **compilar**.  

2.  Clique com botão direito do **vendas pela Internet AW** projeto > **implantar**.

    Durante a implantação no Azure Analysis Services, você será solicitado a inserir sua conta. Insira sua conta organizacional e senha, por exemplo nancy@adventureworks.com. Essa conta deve ser na lista Admins no servidor.
  
    A caixa de diálogo implantar aparece e exibe o status da implantação dos metadados e cada tabela incluída no modelo.  
    
    ![as-lesson13-deploy-status](../tutorial-tabular-1400/media/as-lesson13-deploy-status.png)
  
3. Quando a implantação for concluída com êxito, continue e clique em **Fechar**.  
  

Esta lição descreve o método mais comum e mais fácil para implantar um modelo tabular do SSDT. Opções avançadas de implantação, como o Assistente de implantação ou automatização com XMLA e AMO fornecem maior flexibilidade, consistência e implantações agendadas. Para obter mais informações, consulte [implantação de solução de modelo Tabular](../tabular-models/tabular-model-solution-deployment-ssas-tabular.md).

## <a name="conclusion"></a>Conclusão  
Parabéns! Você terminou a criar e implantar seu primeiro modelo de tabela do Analysis Services. Este tutorial ajudou você a concluir as tarefas mais comuns da criação de um modelo de tabela. Agora que o Modelo de Vendas pela Internet do Adventure Works está implantado, você pode usar o SQL Server Management Studio para gerenciar o modelo; crie scripts de processo e um plano de backup. Os usuários agora também podem se conectar ao modelo usando um aplicativo cliente de relatório, como o Microsoft Excel ou Power BI.  

![ssms como lesson13](../tutorial-tabular-1400/media/as-lesson13-ssms.png)
  
  
  
## <a name="whats-next"></a>O que vem a seguir?
[Conectar-se com o Power BI Desktop](https://docs.microsoft.com/azure/analysis-services/analysis-services-connect-pbi)   
[Lição suplementar - segurança dinâmica](../tutorial-tabular-1400/as-supplemental-lesson-dynamic-security.md)   
[Lição suplementar - linhas de detalhes](../tutorial-tabular-1400/as-supplemental-lesson-detail-rows.md)   
[Lição suplementar – hierarquias desbalanceadas](../tutorial-tabular-1400/as-supplemental-lesson-ragged-hierarchies.md)   
