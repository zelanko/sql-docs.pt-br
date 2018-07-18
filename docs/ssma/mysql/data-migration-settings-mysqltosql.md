---
title: Configurações de migração de dados (MySQLToSQL) | Microsoft Docs
ms.prod: sql
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
applies_to:
- Azure SQL Database
- SQL Server
ms.assetid: 9c396df4-5676-4f32-9c57-70d4f15f9b7a
caps.latest.revision: 9
author: Shamikg
ms.author: Shamikg
manager: craigg
ms.openlocfilehash: a5590adadc1436d616d73b275ad90359b6e64d88
ms.sourcegitcommit: c7a98ef59b3bc46245b8c3f5643fad85a082debe
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/12/2018
ms.locfileid: "38984598"
---
# <a name="data-migration-settings-mysqltosql"></a>Configurações de migração de dados (MySQLToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**Configurações de migração de dados** permite que o usuário escreva consultas personalizadas para a migração de dados.  
  
-   Essa guia está disponível quando **estendido opções de migração de dados** é definido como **mostram** e ficará oculto quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre as configurações do projeto de migração, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/2a3cba9e-cd54-4a8b-b858-8fc4cf2580d9) .  
  
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
  
-   **Aplicar:** clique em **aplicar** para aplicar as configurações que foram alteradas.  
  
-   **Cancelar:** clique em **Cancelar** para restaurar as configurações presentes antes que as alterações estavam sendo feitas.  
  
## <a name="see-also"></a>Consulte também  
[Migração de dados MySQL para o SQL Server/SQL Azure](http://msdn.microsoft.com/a6a7f4d6-68aa-4a38-93bf-53eba0d7dc82)  
  
