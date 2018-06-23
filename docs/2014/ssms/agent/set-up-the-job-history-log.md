---
title: Configurar o log do histórico do trabalho | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- dbe-cross-instance
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: 018e5c49-d3a0-4504-851a-f70996a34bb7
caps.latest.revision: 22
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 206f25645a0b00829f76d45c497938d29a9775cb
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36010133"
---
# <a name="set-up-the-job-history-log"></a>Set Up the Job History Log
  Este tópico descreve como configurar o log de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent.  
  
-   **Antes de começar:**  [Segurança](#Security)  
  
-   **Para configurar o histórico do trabalho de log, usando:**[SQL Server Management Studio  ](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
 **Para configurar o log do histórico do trabalho**  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)]e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Na caixa de diálogo **Propriedades do SQL Server Agent** , selecione a página **Histórico** .  
  
4.  Escolha entre as seguintes opções:  
  
    1.  Marque **Limitar tamanho do log do histórico de trabalho**e indique o número máximo de linhas para o log de histórico de trabalhos e o número máximo de linhas por trabalho.  
  
    2.  Marque **Remover automaticamente o histórico do agente**e especifique um período de tempo, para que os históricos anteriores a ele sejam excluídos do log.  
  
## <a name="see-also"></a>Consulte também  
 [Implementar trabalhos](implement-jobs.md)   
 [Monitorar atividade do trabalho](monitor-job-activity.md)   
 [Criar trabalhos](create-jobs.md)  
  
  