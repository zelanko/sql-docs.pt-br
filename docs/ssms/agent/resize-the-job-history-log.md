---
title: "Redimensionar o log do histórico do trabalho | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- jobs [SQL Server Agent], history
- resizing job history log
- size [SQL Server], job history log
- logs [SQL Server], jobs
- SQL Server Agent jobs, history
- historical information [SQL Server], jobs
ms.assetid: ddee1ce8-9d1b-4017-9894-bf7256aed95d
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: HT
ms.sourcegitcommit: 47182ebd082dfae0963d761e54c4045be927d627
ms.openlocfilehash: 77a39273f5fa02bac3255ea0436341db2342c236
ms.contentlocale: pt-br
ms.lasthandoff: 07/11/2017

---
# <a name="resize-the-job-history-log"></a>Resize the Job History Log
Este tópico descreve como definir os limites de tamanho para logs de histórico de trabalhos do [!INCLUDE[msCoName](../../includes/msconame_md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent usando o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull_md.md)].
  
-   **Antes de começar:**  
  
    [Segurança](#Security)  
  
-   **Para definir limites de tamanho para logs de histórico de trabalho, usando:**  
  
    [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
  
#### <a name="to-resize-the-job-history-log-based-on-raw-size"></a>Para redimensionar o log do histórico do trabalho segundo um tamanho bruto  
  
1.  No **Pesquisador de Objetos** , conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e a expanda.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Selecione a página **Histórico** e confirme se a opção **Limitar tamanho do log do histórico de trabalhos**está marcada.  
  
4.  Na caixa **Tamanho máximo do log do histórico de trabalho** , insira o número máximo de linhas que o log de histórico do trabalho deve permitir.  
  
5.  Na caixa **Máximo de linhas do log do histórico de trabalho por trabalho** , insira o número máximo de linhas que o log de histórico do trabalho deve permitir para um trabalho.  
  
#### <a name="to-resize-the-job-history-log-based-on-time"></a>Para redimensionar o log de histórico de trabalho segundo o tempo  
  
1.  No **Pesquisador de Objetos**, conecte-se a uma instância do [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion_md.md)]e expanda-a.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**e então clique em **Propriedades**.  
  
3.  Selecione a página **Histórico** e clique em **Remover automaticamente o histórico do agente**.  
  
4.  Selecione o número apropriado de **Dia(s)**, **Semana(s)**ou **Mês (meses)**.  
  

