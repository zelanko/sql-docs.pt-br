---
title: Forçar um servidor de destino a sondar o servidor mestre | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- forcing master server polling
- polling master servers [SQL Server]
- master servers [SQL Server], polling
- target servers [SQL Server], polling the master server
ms.assetid: f1189a47-5ac3-45e2-9c5f-847810672279
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 7e9580839c18ed40a6163ab933ce40276bc413ab
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63044051"
---
# <a name="force-a-target-server-to-poll-the-master-server"></a>Forçar um servidor de destino a sondar o servidor mestre
  Este tópico descreve como obrigar um servidor de destino a sondar o servidor mestre. O servidor de destino deve estar registrado no servidor mestre.  
  
 Um trabalho é uma série especificada de ações que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent executa. Um trabalho multisservidor é um trabalho executado por um servidor mestre em um ou mais servidores de destino. Cada servidor de destino pode executar uma instância do mesmo trabalho ao mesmo tempo. Cada servidor de destino sonda o servidor mestre periodicamente, baixa uma cópia dos eventuais trabalhos novos a ele atribuídos e, em seguida, desconecta-se. O servidor de destino executa o trabalho localmente e, depois, reconecta-se ao servidor mestre para carregar o status do resultado do trabalho.  
  
> [!NOTE]  
>  Se o servidor mestre não estiver acessível quando o servidor de destino tentar carregar o status do trabalho, este será colocado em spool até que o servidor mestre esteja novamente acessível.  
  
-   **Antes de começar:**  [Limitações e Restrições](#Restrictions), [Segurança](#Security)  
  
-   **Para forçar um servidor de destino a sondar o servidor mestre, usando:**  [SQL Server Management Studio](#SSMS)  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Restrictions"></a> Limitações e restrições  
 O servidor de destino deve estar registrado no servidor mestre. Você deve executar as instruções fornecidas neste tópico do servidor mestre.  
  
###  <a name="Security"></a> Segurança  
 Para obter informações detalhadas, consulte [Implement SQL Server Agent Security](implement-sql-server-agent-security.md) e [Choose the Right SQL Server Agent Service Account for Multiserver Environments](choose-the-right-sql-server-agent-service-account-for-multiserver-environments.md).  
  
##  <a name="SSMS"></a> Usando o SQL Server Management Studio  
 **Para forçar um servidor de destino a sondar o servidor mestre**  
  
1.  No **Pesquisador de Objetos**, expanda o servidor mestre.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent**, aponte para **Administração Multisservidor**e clique em **Gerenciar Servidores de Destino**.  
  
3.  Clique em um servidor de destino e, em seguida, em **Forçar Sondagem**.  
  
  
