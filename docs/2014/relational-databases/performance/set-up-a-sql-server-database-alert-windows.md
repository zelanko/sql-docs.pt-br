---
title: Configurar um alerta de banco de dados do SQL Server (Windows) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- alerts [SQL Server], creating
ms.assetid: 65d2c5c1-921f-4eff-9ef7-149170ab61e8
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 3342af1de84e922ce63848c8fdffe5aa30ec309a
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63150494"
---
# <a name="set-up-a-sql-server-database-alert-windows"></a>Configurar um alerta de banco de dados do SQL Server (Windows)
  Usando o Monitor do Sistema, é possível criar um alerta a ser emitido quando um valor-limite de um contador do Monitor do Sistema for atingido. Em resposta ao alerta, o Monitor do Sistema pode iniciar um aplicativo, tal como um aplicativo personalizado escrito para lidar com a condição de alerta. Por exemplo, você pode criar um alerta a ser emitido quando o número de deadlocks exceder um valor específico.  
  
 Os alertas também podem ser definidos usando o Microsoft [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] e o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent. Para obter mais informações, consulte [Alertas](../../ssms/agent/alerts.md).  
  
### <a name="to-set-up-a-sql-server-database-alert"></a>Para configurar um alerta de banco de dados do SQL Server  
  
1.  Na árvore de navegação da janela Desempenho, expanda **Logs e Alertas de Desempenho**.  
  
2.  Clique com o botão direito do mouse em **Alertas**e clique em **Novas Configurações de Alerta**.  
  
3.  Na caixa de diálogo **Novas Configurações de Alerta** , digite um nome para o novo alerta e clique em **OK**.  
  
4.  Na guia **Geral** da caixa de diálogo do novo alerta, adicione um **Comentário**e clique em **Adicionar** para adicionar um contador ao alerta.  
  
     Todos os alertas devem ter pelo menos um contador.  
  
5.  Na caixa de diálogo Adicionar Contadores, selecione um objeto do SQL Server na lista **Objeto de Desempenho** e um contador em **Selecionar contadores na lista**.  
  
6.  Para adicionar o contador ao alerta, clique em **Adicionar**. Você pode continuar adicionando contadores ou clicar em **Fechar** para retornar à caixa de diálogo do novo alerta.  
  
7.  Na caixa de diálogo do novo alerta, clique em **Acima** ou **Abaixo**na lista **Alertar quando o valor estiver** e insira um valor-limite em **Limite**.  
  
     O alerta será gerado quando o valor do contador estiver acima ou abaixo do valor-limite (segundo a opção por **Acima** ou **Abaixo**).  
  
8.  Nas caixas **Amostrar dados a cada** , defina a frequência de amostragem.  
  
9. Na guia **Ação** , defina as ações que devem ocorrer sempre que o alerta for disparado.  
  
10. Na guia **Agendar** , defina o agendamento de início e interrupção da verificação do alerta.  
  
## <a name="see-also"></a>Consulte também  
 [Criar um alerta de banco de dados do SQL Server](../performance-monitor/create-a-sql-server-database-alert.md)  
  
  
