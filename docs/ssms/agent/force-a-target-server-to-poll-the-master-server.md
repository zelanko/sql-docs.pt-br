---
title: "Forçar um servidor de destino a sondar o servidor mestre | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-agent
ms.reviewer: 
ms.suite: sql
ms.technology: tools-ssms
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
caps.latest.revision: "4"
author: stevestein
ms.author: sstein
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: b8f926c927122567a6ec8bcc40bb9945c0473936
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Force a Target Server to Poll the Master Server
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)] Este tópico descreve como forçar um servidor de destino a sondar o servidor mestre. O servidor de destino deve estar registrado no servidor mestre.  
  
Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent executa. Um trabalho multisservidor é um trabalho executado por um servidor mestre em um ou mais servidores de destino. Cada servidor de destino pode executar uma instância do mesmo trabalho ao mesmo tempo. Cada servidor de destino sonda o servidor mestre periodicamente, baixa uma cópia dos eventuais trabalhos novos a ele atribuídos e, em seguida, desconecta-se. O servidor de destino executa o trabalho localmente e, depois, reconecta-se ao servidor mestre para carregar o status do resultado do trabalho.  
  
> [!NOTE]  
> Se o servidor mestre não estiver acessível quando o servidor de destino tentar carregar o status do trabalho, este será colocado em spool até que o servidor mestre esteja novamente acessível.  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para forçar um servidor de destino a sondar o servidor mestre usando:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
O servidor de destino deve estar registrado no servidor mestre. Você deve executar as instruções fornecidas neste tópico do servidor mestre.  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) e [Choose the Right SQL Server Agent Service Account for Multiserver Environments](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
**Para forçar um servidor de destino a sondar o servidor mestre**  
  
1.  No **Pesquisador de Objetos**, expanda o servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Gerenciar Servidores de Destino**.  
  
3.  Clique em um servidor de destino e, em seguida, em **Forçar Sondagem**.  
  
