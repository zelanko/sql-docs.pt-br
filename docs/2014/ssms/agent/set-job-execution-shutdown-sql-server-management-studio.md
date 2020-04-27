---
title: Definir o desligamento da execução de trabalhos (SQL Server Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: ssms
ms.topic: conceptual
helpviewer_keywords:
- jobs [SQL Server Agent], stopping
- SQL Server Agent jobs, stopping
- stopping jobs
- SQL Server Agent jobs, execution shutdowns
ms.assetid: ac23e88f-53fc-41de-bb16-0c27c002d5a5
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: ca9343fe8a6f9e89ba9f26dbbbb12dd7362aff91
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "63033592"
---
# <a name="set-job-execution-shutdown-sql-server-management-studio"></a>Set Job Execution Shutdown (SQL Server Management Studio)
  Este tópico descreve como definir o tempo que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent aguardará até que os trabalhos em execução [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] sejam concluídos antes [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] que o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)]próprio agente seja concluído no usando o.  
  
 **Neste tópico**  
  
-   **Antes de começar:**  
  
     [Segurança](#Security)  
  
-   **Para definir um tempo de desligamento para um trabalho do SQL Server Agent, usando:**  
  
     [SQL Server Management Studio](#SSMSProcedure)  
  
##  <a name="before-you-begin"></a><a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="security"></a><a name="Security"></a> Segurança  
  
####  <a name="permissions"></a><a name="Permissions"></a> Permissões  
 Por padrão, os membros da função de servidor fixa **sysadmin** podem marcar a hora que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent esperará pela conclusão de trabalhos em execução antes que o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent finalize-os. Deve ser concedida a outros usuários uma das seguintes funções de banco de dados fixas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent no banco de dados **msdb** :  
  
-   **SQLAgentUserRole**  
  
-   **SQLAgentReaderRole**  
  
-   **SQLAgentOperatorRole**  
  
##  <a name="using-sql-server-management-studio"></a><a name="SSMSProcedure"></a> Usando o SQL Server Management Studio  
  
#### <a name="to-set-job-execution-shutdown"></a>Para definir desligamento de execução de trabalho  
  
1.  No **Pesquisador de Objetos** , clique no sinal de adição para expandir o servidor no qual você deseja definir um intervalo de desligamento de execução de trabalho.  
  
2.  Clique com o botão direito do mouse em **SQL Server Agent** e selecione **Propriedades**.  
  
3.  Em **Selecione uma página**, selecione **Sistema de Trabalho**.  
  
4.  Defina o **Intervalo de tempo limite de desligamento** em segundos para aumentar ou diminuir o intervalo do tempo limite para o desligamento. Isso determina quanto tempo o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent aguardará pelo término dos trabalhos em execução antes de o próprio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent terminar.  
  
  
