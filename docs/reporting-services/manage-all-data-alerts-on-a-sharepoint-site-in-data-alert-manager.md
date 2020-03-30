---
title: Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados | Microsoft Docs
ms.date: 08/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 9c70b0f4-2db8-4c2e-acbf-96e2a55ddc48
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016||=sqlallproducts-allversions'
ms.openlocfilehash: 9702ca84fab0da2024db6f6f5e0f510822dcd29e
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "65579805"
---
# <a name="manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager"></a>Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados

[!INCLUDE[ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE[ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE[ssrs-appliesto-not-pbirsi](../includes/ssrs-appliesto-not-pbirs.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)]

Os administradores de alerta do SharePoint podem exibir uma lista dos alertas de dados criados por qualquer usuário do site e informações sobre os alertas. Os administradores de alerta também podem excluir alertas. A imagem a seguir mostra os recursos disponíveis para os administradores de alerta no Gerenciador de Alerta de Dados.

 ![Gerenciador de Alertas para administradores do site do SharePoint](../reporting-services/media/rs-alertmanagersite.gif "Gerenciador de Alertas para administradores do site do SharePoint")

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

## <a name="view-a-list-of-alerts-created-by-a-site-user"></a>Exibir uma lista de alertas criados por um usuário do site  
  
1.  Vá para o site do SharePoint onde as definições de alertas de dados são salvas.  
  
2.  Na home page, clique em **Ações do Site**.  
  
3.  Role para a parte inferior da lista e clique em **Configurações de Site**.  
  
4.  No **Reporting Services**, clique em **Gerenciar Alertas de Dados**.  
  
5.  Clique na seta para baixo na lista **Exibir alertas de usuário** e selecione o usuário cujos alertas você deseja exibir.  
  
6.  Clique na seta para baixo ao lado de **Exibir alertas de relatório** e selecione um alerta específico a ser exibido ou clique em **Mostrar Tudo** para listar todos os alertas criados pelo usuário selecionado.  
  
     Uma tabela lista o nome do alerta, o nome do relatório, o nome da pessoa que criou o alerta de dados, o número de vezes em que o alerta de dados foi enviado, a última vez que a definição do alerta de dados foi modificada e o status do alerta de dados. Se o alerta de dados não puder ser gerado ou enviado, a coluna de status conterá informações sobre o erro e ajudará você a solucionar o problema.  
  
## <a name="delete-an-alert-definition"></a>Excluir uma definição de alerta  
  
-   Clique com o botão direito do mouse no alerta de dados que você deseja excluir e clique em **Excluir**.  
  
    > [!NOTE]  
    >  Depois que você excluir o alerta, nenhuma mensagem de alerta adicional será enviada. No entanto, se você consultar o banco de dados de alertas, talvez descubra que a definição de alerta ainda existe. O serviço de alerta executa a limpeza de acordo com uma agenda e a definição de alerta será excluída permanentemente na próxima limpeza. O intervalo de limpeza padrão é de 20 minutos. Esse e outros intervalos de limpeza são configuráveis. Para obter mais informações, consulte [Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)[Alertas de dados do Reporting Services].  

## <a name="see-also"></a>Consulte Também

[Gerenciador de Alertas de dados para administradores de alertas](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
