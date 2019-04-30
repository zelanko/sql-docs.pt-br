---
title: Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- managing, alerts
- managing, data alerts
ms.assetid: 9c70b0f4-2db8-4c2e-acbf-96e2a55ddc48
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: d0fa7051bbbbc95b1fac5c0990b8210c6198be69
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63279018"
---
# <a name="manage-all-data-alerts-on-a-sharepoint-site-in-data-alert-manager"></a>Gerenciar todos os alertas de dados em um site do SharePoint no Gerenciador de Alertas de Dados
  Os administradores de alerta do SharePoint podem exibir uma lista dos alertas de dados criados por qualquer usuário do site e informações sobre os alertas. Os administradores de alerta também podem excluir alertas. A imagem a seguir mostra os recursos disponíveis para os administradores de alerta no Gerenciador de Alerta de Dados.  
  
 ![Gerenciador de Alertas para administradores de site do SharePoint](media/rs-alertmanagersite.gif "Alert Manager for SharePoint site administrators")  
  
### <a name="to-view-a-list-of-alerts-created-by-a-site-user"></a>Para exibir uma lista dos alertas criados por um usuário de site  
  
1.  Vá para o site do SharePoint onde as definições de alertas de dados são salvas.  
  
2.  Na home page, clique em **Ações do Site**.  
  
3.  Role para a parte inferior da lista e clique em **Configurações de Site**.  
  
4.  No **Reporting Services**, clique em **Gerenciar Alertas de Dados**.  
  
5.  Clique na seta para baixo na lista **Exibir alertas de usuário** e selecione o usuário cujos alertas você deseja exibir.  
  
6.  Clique na seta para baixo ao lado de **Exibir alertas de relatório** e selecione um alerta específico a ser exibido ou clique em **Mostrar Tudo** para listar todos os alertas criados pelo usuário selecionado.  
  
     Uma tabela lista o nome do alerta, o nome do relatório, o nome da pessoa que criou o alerta de dados, o número de vezes em que o alerta de dados foi enviado, a última vez que a definição do alerta de dados foi modificada e o status do alerta de dados. Se o alerta de dados não puder ser gerado ou enviado, a coluna de status conterá informações sobre o erro e ajudará você a solucionar o problema.  
  
### <a name="to-delete-an-alert-definition"></a>Para excluir uma definição de alerta  
  
-   Clique com o botão direito do mouse no alerta de dados que você deseja excluir e clique em **Excluir**.  
  
    > [!NOTE]  
    >  Depois que você excluir o alerta, nenhuma mensagem de alerta adicional será enviada. No entanto, se você consultar o banco de dados de alertas, talvez descubra que a definição de alerta ainda existe. O serviço de alerta executa a limpeza de acordo com uma agenda e a definição de alerta será excluída permanentemente na próxima limpeza. O intervalo de limpeza padrão é de 20 minutos. Esse e outros intervalos de limpeza são configuráveis. Para obter mais informações, consulte [Reporting Services Data Alerts](../ssms/agent/alerts.md)[Alertas de dados do Reporting Services].  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de Alertas de dados para administradores de alertas](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Reporting Services Data Alerts](../ssms/agent/alerts.md)  
  
  
