---
title: Editar um alerta de dados no Designer de Alertas | Microsoft Docs
description: Saiba como editar um alerta de dados. Você pode editar os alertas de dados acessando-os no Gerenciador de Alertas de Dados.
ms.date: 07/02/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: reporting-services
ms.topic: conceptual
helpviewer_keywords:
- editing, data alerts
- updating, data alerts
- editing, alerts
- updating, alerts
ms.assetid: dde3664d-90b5-4b12-969e-39152c86e58a
author: maggiesMSFT
ms.author: maggies
monikerRange: '>=sql-server-2016 <=sql-server-2016'
ms.openlocfilehash: b97a4a51a8edbce4172b92fee7a418b38ce42bc4
ms.sourcegitcommit: 1a544cf4dd2720b124c3697d1e62ae7741db757c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/14/2020
ms.locfileid: "97472537"
---
# <a name="edit-a-data-alert-in-alert-designer"></a>Editar um alerta de dados no Designer de Alertas

[!INCLUDE [ssrs-appliesto](../includes/ssrs-appliesto.md)] [!INCLUDE [ssrs-appliesto-2016](../includes/ssrs-appliesto-2016.md)] [!INCLUDE [ssrs-appliesto-not-2017](../includes/ssrs-appliesto-not-2017.md)] [!INCLUDE[ssrs-appliesto-sharepoint-2013-2016i](../includes/ssrs-appliesto-sharepoint-2013-2016.md)] [!INCLUDE [ssrs-appliesto-not-pbirs](../includes/ssrs-appliesto-not-pbirs.md)]

[!INCLUDE [ssrs-previous-versions](../includes/ssrs-previous-versions.md)]

Você abre a definição de alerta de dados que deseja editar no Gerenciador de Alertas de Dados. Apenas o usuário que criou a definição de alerta pode editá-la. Para obter mais informações sobre como abrir o Gerenciador de Alertas de Dados, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](../reporting-services/manage-my-data-alerts-in-data-alert-manager.md).

> [!NOTE]
> A integração do Reporting Services ao SharePoint não está mais disponível após o SQL Server 2016.

 A imagem a seguir mostra o menu de contexto em um alerta de dados no Gerenciador de Alertas de Dados.  
  
 ![Abrir o Designer de Alertas de Dados clicando em Editar](../reporting-services/media/rs-alertmanageriwopendesigner.gif "Abrir o Designer de Alertas de Dados clicando em Editar")  
  
 O procedimento a seguir inclui as etapas para abrir a definição de alerta para edição no Designer de Alertas de Dados no Gerenciador de Alertas de Dados.  
  
### <a name="to-edit-a-data-alert-definition-in-data-alert-designer"></a>Para editar uma definição de alerta de dados no Designer de Alertas de Dados  
  
1.  No Gerenciador de Alertas de Dados, clique com o botão direito do mouse na definição de alerta de dados que você deseja editar e clique em **Editar**.  
  
     A definição de alerta é aberta no Designer de Alertas de Dados.  
  
2.  Atualize as regras, as configurações de agenda e as configurações de email. Para obter mais informações, consulte [Designer de Alertas de Dados](../reporting-services/data-alert-designer.md) e [Criar um Alerta de Dados no Designer de Alertas de Dados](../reporting-services/create-a-data-alert-in-data-alert-designer.md).  
  
    > [!NOTE]  
    >  Você não pode escolher um feed de dados diferente. Para usar um feed de dados diferente, você deve criar uma nova definição de alerta de dados.  
  
3.  Clique em **Save** (Salvar).  
  
    > [!NOTE]  
    >  Se o relatório tiver sido alterado e os feeds de dados gerados no relatório tiverem sido alterados, a definição de alerta talvez não seja mais válida. Isso ocorre quando uma coluna referenciada pela definição de alerta nas regras é excluída do relatório ou altera o tipo de dados, ou quando o relatório é excluído ou movido. Você pode abrir uma definição de alerta que não é válida, mas só pode salvá-la novamente depois que ela estiver válida com base na versão atual do feed de dados de relatório do qual ela depende. Para saber mais sobre como os feeds de dados são gerados com base em relatórios, consulte [Gerando feeds de dados com base em relatórios &#40;Construtor de Relatórios e SSRS&#41;](../reporting-services/report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  

## <a name="see-also"></a>Consulte Também

[Gerenciador de Alertas de dados para administradores de alertas](../reporting-services/data-alert-manager-for-alerting-administrators.md)   
[Reporting Services Data Alerts](../reporting-services/reporting-services-data-alerts.md)  

Mais perguntas? [Experimente perguntar no fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
