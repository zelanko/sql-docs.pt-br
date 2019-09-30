---
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
ms.openlocfilehash: 9aa748fff6c0986290267815b90b43fd8fecb6b1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71294650"
---
# <a name="oracle-credentials-for-running-script"></a>Credenciais Oracle para executar script

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  Para executar o script de log suplementar do console do Oracle CDC Designer, o programa solicita as credenciais do usuário Oracle que está executando o script. Para executar este script, o usuário Oracle deve ter permissão ALTER TABLE para todas as tabelas a serem capturadas e permissão SELECT na exibição DBA_LOG_GROUPS.  
  
## <a name="task-list"></a>Lista de Tarefas  
 Insira o seguinte nesta caixa de diálogo:  
  
 **Autenticação**  
  
 Selecione uma destas opções:  
  
-   **Autenticação do Windows**: Selecione essa opção para usar as credenciais de domínio atuais do Windows. Você só poderá usar esta opção se o banco de dados Oracle estiver configurado para funcionar com autenticação do Windows.  
  
-   **Autenticação do Oracle**: Se você selecionar essa opção, precisará digitar o **Nome de Usuário** e a **Senha** no banco de dados de origem do Oracle ao qual você está se conectando.  
  
## <a name="see-also"></a>Consulte Também  
 [Como gerenciar uma instância CDC](../../integration-services/change-data-capture/how-to-manage-a-cdc-instance.md)   
 [Examinar e gerar scripts de log suplementares](../../integration-services/change-data-capture/review-and-generate-supplemental-logging-scripts.md)  
  
  
