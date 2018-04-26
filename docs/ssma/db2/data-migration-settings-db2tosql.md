---
title: Configurações de migração de dados (DB2ToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-db2
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology:
- sql-ssma
ms.tgt_pltfrm: ''
ms.topic: article
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 573e673e-a194-4cb2-9aba-aaac6e1a225c
caps.latest.revision: 4
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 49f254e86891bafb14e6e250f7ac9f155180bb9e
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="data-migration-settings-db2tosql"></a>Configurações de migração de dados (DB2ToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**As configurações de migração de dados** permite que o usuário escreva consultas personalizadas para a migração de dados.  
  
-   Essa guia está disponível quando **estendidos opções de migração de dados** é definido como **Mostrar** e ficará oculto quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre configurações de projeto de migração, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/en-us/48aaa8e6-a9cb-487d-9ba5-fc3f1c4786ae) .  
  
-   Análise de instruções SQL personalizada será implementado em **as configurações de migração de dados** guia do nó de tabela.  
  
-   A seguir está as duas caixas de seleção disponíveis no **as configurações de migração de dados** viz.:  
  
    1.  Truncar a tabela do SQL Server  
  
    2.  Selecione Usar personalizado  
  
1.  **Truncar a tabela do SQL Server:**  
     Essa opção permite que o usuário tenha uma visão clara dos dados migrados no banco de dados de destino.  
  
    -   Por padrão, esta caixa de texto é verificada.  
  
    -   Se esta caixa de texto não estiver marcada, os dados migrados serão adicionados para os dados existentes no banco de dados de destino.  
  
2.  **Selecione Usar personalizado:**  
     Essa opção permite que o usuário modifique o **selecione** instrução presente (**selecione** instrução permite que os usuários selecionar os dados a serem exibidos no banco de dados de destino).  
  
    1.  Por padrão, esta caixa de texto está desmarcada.  
  
    2.  Se esta caixa de texto é verificada, ele permite que os usuários modifiquem o **selecione** instrução presente.  
  
Há dois botões presentes viz.:  
  
-   **Aplicar:** clique **aplicar** para aplicar as configurações que foram alteradas.  
  
-   **Cancelar:** clique **Cancelar** para restaurar as configurações presentes antes que as alterações sejam feitas.  
  
## <a name="see-also"></a>Consulte também  
[Migração de dados DB2 para o SQL Server](http://msdn.microsoft.com/en-us/86cbd39f-6dac-409a-9ce1-7dd54403f84b)  
  
