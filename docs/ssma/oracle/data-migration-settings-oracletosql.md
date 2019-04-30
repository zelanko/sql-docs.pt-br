---
title: Configurações de migração de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 96b60573b81625c8896fb9022a6a718770f349ed
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63287178"
---
# <a name="data-migration-settings-oracletosql"></a>Configurações de migração de dados (OracleToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**Configurações de migração de dados** permite que o usuário escreva consultas personalizadas para a migração de dados.  
  
-   Essa guia está disponível quando **estendido opções de migração de dados** é definido como **mostram** e ficará oculto quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações do projeto de migração, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
-   Análise de instruções SQL personalizadas será implementado no **configurações de migração de dados** guia da tabela de nó.  
  
-   A seguir está as duas caixas de seleção disponíveis na **configurações de migração de dados** sobre visualização.:  
  
    1.  Truncar a tabela do SQL Server  
  
    2.  Selecione uso personalizado  
  
1.  **Trunca a tabela do SQL Server:**  
     Essa opção permite que o usuário tenha uma visão clara dos dados migrados no banco de dados de destino.  
  
    -   Por padrão, essa caixa de texto é verificada.  
  
    -   Se essa caixa de texto é desmarcada, em seguida, os dados que são migrados serão adicionados para os dados existentes no banco de dados de destino.  
  
2.  **Selecione uso personalizado:**  
     Essa opção permite que o usuário modifique os **selecionar** instrução presente (**selecione** instrução permite que os usuários selecionar os dados a ser exibido no banco de dados de destino).  
  
    1.  Por padrão, essa caixa de texto está desmarcada.  
  
    2.  Se essa caixa de texto é verificada, ele permite que os usuários modifiquem o **selecionar** instrução presente.  
  
Há dois botões presentes sobre visualização.:  
  
-   **Apply:** Clique em **aplicar** para aplicar as configurações que foram alteradas.  
  
-   **Cancelar:** Clique em **Cancelar** para restaurar as configurações presentes antes que as alterações estavam sendo feitas.  
  
## <a name="see-also"></a>Consulte também  
[Migração de dados Oracle para o SQL Server](migrating-oracle-data-into-sql-server-oracletosql.md)  
  
