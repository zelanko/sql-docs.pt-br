---
title: Credenciais Oracle para executar scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.component: change-data-capture
ms.reviewer: ''
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
caps.latest.revision: 7
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: bfc711c1e807da47d4c440fe0ed4460d776e6437
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="oracle-credentials-for-running-script"></a>Credenciais Oracle para executar script
  Para executar o script de log suplementar do console do Oracle CDC Designer, o programa solicita as credenciais do usuário Oracle que está executando o script. Para executar este script, o usuário Oracle deve ter permissão ALTER TABLE para todas as tabelas a serem capturadas e permissão SELECT na exibição DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Insira o seguinte nesta caixa de diálogo:  
  
 **Autenticação**  
  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**: selecione isto para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: se você selecionou esta opção, deve digitar o **Nome de usuário** e **Senha** para o usuário no banco de dados Oracle de origem ao qual você está se conectando.  
  
## <a name="see-also"></a>Consulte Também  
 [Como gerenciar uma instância CDC](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Examinar e gerar scripts de log suplementares](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
