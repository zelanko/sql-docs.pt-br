---
title: "Forçar um servidor de destino a sondar o servidor mestre | Microsoft Docs"
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
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
caps.latest.revision: 4
author: stevestein
ms.author: sstein
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: 57fe0392adfb1e290491815acd216fd356e20f3e
ms.contentlocale: pt-br
ms.lasthandoff: 04/11/2017

---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Forçar um servidor de destino a sondar o servidor mestre
Este tópico descreve como obrigar um servidor de destino a sondar o servidor mestre. O servidor de destino deve estar registrado no servidor mestre.  
  
Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion_md.md)] Agent executa. Um trabalho multisservidor é um trabalho executado por um servidor mestre em um ou mais servidores de destino. Cada servidor de destino pode executar uma instância do mesmo trabalho ao mesmo tempo. Cada servidor de destino sonda o servidor mestre periodicamente, baixa uma cópia dos eventuais trabalhos novos a ele atribuídos e, em seguida, desconecta-se. O servidor de destino executa o trabalho localmente e, depois, reconecta-se ao servidor mestre para carregar o status do resultado do trabalho.  
  
> [!NOTE]  
> Se o servidor mestre não estiver acessível quando o servidor de destino tentar carregar o status do trabalho, este será colocado em spool até que o servidor mestre esteja novamente acessível.  
  
-   **Antes de começar:**  [Limitações e restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para forçar um servidor de destino a sondar o servidor mestre usando:** [SQL Server Management Studio](#SSMS)  
  
## <a name="BeforeYouBegin"></a>Antes de começar  
  
### <a name="Restrictions"></a>Limitações e restrições  
O servidor de destino deve estar registrado no servidor mestre. Você deve executar as instruções fornecidas neste tópico do servidor mestre.  
  
### <a name="Security"></a>Segurança  
Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](../../ssms/agent/implement-sql-server-agent-security.md) e [Escolher a conta de serviço do SQL Server Agent certa para ambientes multisservidor](../../ssms/agent/choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
## <a name="SSMS"></a>Usando o SQL Server Management Studio  
**Para forçar um servidor de destino a sondar o servidor mestre**  
  
1.  No **Pesquisador de Objetos**, expanda o servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Gerenciar Servidores de Destino**.  
  
3.  Clique em um servidor de destino e, em seguida, em **Forçar Sondagem**.  
  

