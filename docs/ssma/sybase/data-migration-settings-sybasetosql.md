---
title: Configurações de migração de dados (SybaseToSQL) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: ssma
ms.topic: conceptual
ms.assetid: 94d7a083-2dbc-4e3d-94dd-92b7ff9d0c2d
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: 1191a29fa3988b85548578e8a38efc12d9fce41c
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63297428"
---
# <a name="data-migration-settings-sybasetosql"></a>Configurações de migração de dados (SybaseToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**Configurações de migração de dados** permite que o usuário escreva consultas personalizadas para a migração de dados.  
  
-   Essa guia está disponível quando **estendido opções de migração de dados** é definido como **mostram** e ficará oculto quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações do projeto de migração, consulte [configurações do projeto (migração)](https://msdn.microsoft.com/82f8857f-7ab1-4738-ab6e-b1e95ea94924) .  
  
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
[Migração de dados Sybase para o SQL Server/SQL Azure](https://msdn.microsoft.com/54a39f5e-9250-4387-a3ae-eae47c799811)  
  
