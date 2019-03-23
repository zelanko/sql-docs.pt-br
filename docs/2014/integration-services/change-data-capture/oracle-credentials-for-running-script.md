---
title: Credenciais Oracle para executar scripts | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 12de97bf147ccb61cde5f82e2fa31782404071e4
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58388804"
---
# <a name="oracle-credentials-for-running-script"></a>Credenciais Oracle para executar script
  Para executar o script de log suplementar do console do Oracle CDC Designer, o programa solicita as credenciais do usuário Oracle que está executando o script. Para executar este script, o usuário Oracle deve ter permissão ALTER TABLE para todas as tabelas a serem capturadas e permissão SELECT na exibição DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Insira o seguinte nesta caixa de diálogo:  
  
 **Autenticação**  
  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**: Selecione essa opção para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: Se você selecionar essa opção, você deve digitar o **nome de usuário** e **senha** para o usuário no banco de dados Oracle de origem, você está se conectando.  
  
## <a name="see-also"></a>Consulte também  
 [Como gerenciar uma instância CDC](manage-a-cdc-instance.md)   
 [Examinar e gerar scripts de log suplementares](review-and-generate-supplemental-logging-scripts.md)  
  
  
