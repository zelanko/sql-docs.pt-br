---
title: Configurar um alerta de banco de dados do SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: performance
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
caps.latest.revision: 23
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 56dcfcc43dfdaf333990ce3f6e95d5aa9bede260
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Configurar um alerta de banco de dados do SQL Server (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o Monitor do Sistema para criar um alerta que é acionado quando um contador do Monitor do Sistema atinge um valor limite. Em resposta ao alerta, o Monitor do Sistema pode iniciar um aplicativo, tal como um aplicativo personalizado escrito para lidar com a condição de alerta. Por exemplo, você pode criar um alerta a ser emitido quando o número de deadlocks exceder um valor específico. 
  
 Os alertas também podem ser definidos pelo uso do Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Alertas](http://msdn.microsoft.com/library/3f57d0f0-4781-46ec-82cd-b751dc5affef).  
  
## <a name="set-up-a-sql-server-database-alert"></a>Configurar um alerta de banco de dados do SQL Server  
  
1. Na árvore de navegação da janela **Desempenho**, expanda **Logs e Alertas de Desempenho**.  
  
2. Clique com o botão direito do mouse em **Alertas** e selecione **Novas Configurações de Alerta**.
  
3. Na caixa de diálogo **Novas Configurações de Alerta**, digite um nome para o novo alerta e selecione **OK**.  
  
4. Na guia **Geral** da caixa de diálogo do novo alerta, adicione um **Comentário**. Selecione **Adicionar** para adicionar um contador ao alerta.  
  
     Todos os alertas devem ter pelo menos um contador.  
  
5. Na caixa de diálogo **Adicionar Contadores**, selecione um objeto do SQL Server na lista **Objeto de Desempenho**. Selecione um contador da lista **Selecionar contadores de**.  
  
6. Para adicionar o contador ao alerta, selecione **Adicionar**. Você pode continuar adicionando contadores ou selecionar **Fechar** para retornar à caixa de diálogo do novo alerta.  
  
7. Na caixa de diálogo do novo alerta, selecione **Acima** ou então **Abaixo** na lista **Alertar quando o valor estiver**. Em seguida, insira um valor limite em **Limite**.  
  
     O alerta será gerado quando o valor do contador estiver acima ou abaixo do valor-limite (segundo a opção por **Acima** ou **Abaixo**).  
  
8. Nas caixas **Amostrar dados a cada** , defina a frequência de amostragem.  
  
9. Na guia **Ação** , defina as ações que devem ocorrer sempre que o alerta for disparado.  
  
10. Na guia **Agendar** , defina o agendamento de início e interrupção da verificação do alerta.  
  
## <a name="see-also"></a>Confira também  
 [Criar um alerta de Banco de Dados do SQL Server](../../relational-databases/performance-monitor/create-a-sql-server-database-alert.md)  
  
  
