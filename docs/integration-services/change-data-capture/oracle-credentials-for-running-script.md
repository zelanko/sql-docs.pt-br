---
description: Credenciais Oracle para executar script
title: Credenciais Oracle para executar scripts | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 4a301cb0-2f5b-41ba-81bf-46b41d07f137
author: chugugrace
ms.author: chugu
ms.openlocfilehash: ba5959cec249da89655d1edb4df8ef8ca225a416
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88426008"
---
# <a name="oracle-credentials-for-running-script"></a>Credenciais Oracle para executar script

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  Para executar o script de log suplementar do console do Oracle CDC Designer, o programa solicita as credenciais do usuário Oracle que está executando o script. Para executar este script, o usuário Oracle deve ter permissão ALTER TABLE para todas as tabelas a serem capturadas e permissão SELECT na exibição DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Insira o seguinte nesta caixa de diálogo:  
  
 **Autenticação**  
  
 Selecione uma das seguintes:  
  
-   **Autenticação do Windows**: selecione isto para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: se você selecionou esta opção, deve digitar o **Nome de usuário** e **Senha** para o usuário no banco de dados Oracle de origem ao qual você está se conectando.  
  
## <a name="see-also"></a>Consulte Também  
 [How to Manage a CDC Instance](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Revisar e gerar scripts de log suplementares](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
