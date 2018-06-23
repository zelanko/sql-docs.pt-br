---
title: Exibir o relatório de envio de logs (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-high-availability
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- viewing log shipping reports
- displaying log shipping reports
- log shipping [SQL Server], monitoring
- log shipping [SQL Server], viewing reports
ms.assetid: 3b549f2f-3683-45e5-b8e8-8095276c41ab
caps.latest.revision: 17
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 8e0118573919f4ad1278bfc6b507769b92fe80ee
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36005700"
---
# <a name="view-the-log-shipping-report-sql-server-management-studio"></a>Exibir o relatório de envio de logs (SQL Server Management Studio)
  Este tópico explica como exibir o relatório de Status de Envio do Log de Transações no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]. Você pode executar um relatório de status em um servidor monitor, servidor primário ou servidor secundário. Para ver as informações mais completas sobre sua configuração de envio de logs, exiba o relatório na instância do servidor monitor.  
  
 O relatório exibe o status de qualquer atividade de envio de logs cujo status esteja disponível a partir da instância de servidor à qual você está conectado. Se essa instância de servidor estiver envolvida em várias configurações em funções diferentes (como servir como monitor para um banco de dados e servidor secundário para outro banco de dados), os resultados exibidos conterão as informações de toda a configuração a partir da perspectiva de cada função. Se o procedimento armazenado puder conectar-se à instância do servidor monitor para uma determinada configuração de envio de logs, o relatório exibirá um status adicional para essa configuração.  
  
 Para cada função executada pela instância de servidor atual, você pode exibir as seguintes informações:  
  
|Role|Informações exibidas|  
|----------|---------------------------|  
|Monitor|O nome e status de todos os servidores primários e servidores secundários que usam essa instância de servidor como servidor monitor.|  
|Primária|Para cada banco de dados primário, o status e nome da instância de servidor atual (como o servidor primário), junto com o nome de banco de dados primário. O relatório exibe o status do trabalho de backup (que é armazenado localmente no servidor primário).<br /><br /> O relatório também contém uma linha para cada um dos servidores secundários correspondentes. Se a configuração usar um servidor monitor e o procedimento armazenado puder conectar-se ao monitor, essas linhas exibirão o status da cópia e o status de restauração do backup de log mais recente.|  
|Secundário|Para cada banco de dados secundário, o status e nome da instância de servidor atual (como o servidor secundário), junto com o nome de banco de dados secundário.<br /><br /> O relatório exibe o status da cópia e trabalhos de restauração no servidor secundário.<br /><br /> O relatório também contém uma linha para o servidor primário correspondente. Se a configuração usar um servidor monitor e o procedimento armazenado puder conectar-se ao monitor, essa linha exibirá o status do backup de log mais recente.|  
  
 As informações exibidas dependerão de a instância de servidor ser um servidor monitor, servidor primário ou servidor secundário. Se as informações não estiverem disponíveis, as células correspondentes ficarão esmaecidas.  
  
 O relatório chama **sp_help_log_shipping_monitor** para obter os dados. Para obter informações sobre as permissões necessárias, consulte [sp_help_log_shipping_monitor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-help-log-shipping-monitor-transact-sql).  
  
### <a name="to-display-the-transaction-log-shipping-status-report-on-a-server-instance"></a>Para exibir o relatório de status de envio do log de transações em uma instância de servidor  
  
1.  Conecte-se a um servidor monitor, servidor primário ou servidor secundário.  
  
2.  Clique com o botão direito do mouse na instância de servidor no Pesquisador de Objetos, aponte para **Relatórios**e aponte para **Relatórios Padrão**.  
  
3.  Clique em **Status de Envio do Log de Transações**.  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o envio de logs &#40;Transact-SQL&#41;](monitor-log-shipping-transact-sql.md)  
  
  
