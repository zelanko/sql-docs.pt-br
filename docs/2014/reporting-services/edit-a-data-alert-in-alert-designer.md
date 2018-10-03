---
title: Editar um alerta de dados no Designer de Alertas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- editing, data alerts
- updating, data alerts
- editing, alerts
- updating, alerts
ms.assetid: dde3664d-90b5-4b12-969e-39152c86e58a
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 511a057721f1dbd8273fe1909c4eaae31dd128f3
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48119436"
---
# <a name="edit-a-data-alert-in-alert-designer"></a>Editar um alerta de dados no Designer de Alertas
  Você abre a definição de alerta de dados que deseja editar no Gerenciador de Alertas de Dados. Apenas o usuário que criou a definição de alerta pode editá-la. Para obter mais informações sobre como abrir o Gerenciador de Alertas de Dados, consulte [Gerenciar meus alertas de dados no Gerenciador de Alertas de Dados](manage-my-data-alerts-in-data-alert-manager.md).  
  
 A imagem a seguir mostra o menu de contexto em um alerta de dados no Gerenciador de Alertas de Dados.  
  
 ![Abrir o Designer de Alerta de Dados clicando em Editar](media/rs-alertmanageriwopendesigner.gif "Abrir o Designer de Alerta de Dados clicando em Editar")  
  
 O procedimento a seguir inclui as etapas para abrir a definição de alerta para edição no Designer de Alertas de Dados no Gerenciador de Alertas de Dados.  
  
### <a name="to-edit-a-data-alert-definition-in-data-alert-designer"></a>Para editar uma definição de alerta de dados no Designer de Alertas de Dados  
  
1.  No Gerenciador de Alertas de Dados, clique com o botão direito do mouse na definição de alerta de dados que você deseja editar e clique em **Editar**.  
  
     A definição de alerta é aberta no Designer de Alertas de Dados.  
  
2.  Atualize as regras, as configurações de agenda e as configurações de email. Para obter mais informações, consulte [Designer de alertas de dados](../../2014/reporting-services/data-alert-designer.md) e [criar um alerta no Designer de alertas de dados](create-a-data-alert-in-data-alert-designer.md).  
  
    > [!NOTE]  
    >  Você não pode escolher um feed de dados diferente. Para usar um feed de dados diferente, você deve criar uma nova definição de alerta de dados.  
  
3.  Clique em **Salvar**.  
  
    > [!NOTE]  
    >  Se o relatório tiver sido alterado e os feeds de dados gerados no relatório tiverem sido alterados, a definição de alerta talvez não seja mais válida. Isso ocorre quando uma coluna referenciada pela definição de alerta nas regras é excluída do relatório ou altera o tipo de dados, ou quando o relatório é excluído ou movido. Você pode abrir uma definição de alerta que não é válida, mas só pode salvá-la novamente depois que ela estiver válida com base na versão atual do feed de dados de relatório do qual ela depende. Para saber mais sobre como os feeds de dados são gerados com base em relatórios, consulte [Gerando feeds de dados com base em relatórios &#40;Construtor de Relatórios e SSRS&#41;](report-builder/generating-data-feeds-from-reports-report-builder-and-ssrs.md).  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciador de alertas de dados para administradores de alerta](../../2014/reporting-services/data-alert-manager-for-alerting-administrators.md)   
 [Alertas de dados do Reporting Services](../ssms/agent/alerts.md)  
  
  
