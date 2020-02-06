---
title: Configurar um alerta de banco de dados do SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f76c6f4f4d65273c35dffb1cb17e664fceac0328
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68113342"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Configurar um alerta de banco de dados do SQL Server (Windows)
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
  Use o Monitor do Sistema para criar um alerta que é acionado quando um contador do Monitor do Sistema atinge um valor limite. Em resposta ao alerta, o Monitor do Sistema pode iniciar um aplicativo, tal como um aplicativo personalizado escrito para lidar com a condição de alerta. Por exemplo, você pode criar um alerta a ser emitido quando o número de deadlocks exceder um valor específico. 
  
 Os alertas também podem ser definidos pelo uso do Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Alertas](../../ssms/agent/alerts.md).  
  
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
  
  
