---
title: Configurações de migração de dados (OracleToSQL) | Microsoft Docs
ms.prod: sql
ms.prod_service: sql-tools
ms.service: ''
ms.component: ssma-oracle
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.technology: ssma
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 91f7f558-025d-4f4d-ac2c-aa095e7d1ace
caps.latest.revision: 3
author: Shamikg
ms.author: Shamikg
manager: v-thobro
ms.openlocfilehash: 2b90d81e07eecf97dc2e8c6f058ae7a278ecef64
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-migration-settings-oracletosql"></a>Configurações de migração de dados (OracleToSQL)
  
## <a name="data-migration-settings"></a>Configurações de migração de dados  
**As configurações de migração de dados** permite que o usuário escreva consultas personalizadas para a migração de dados.  
  
-   Essa guia está disponível quando **estendidos opções de migração de dados** é definido como **Mostrar** e ficará oculto quando a configuração é definida como **ocultar** nas configurações do projeto. Para obter mais informações sobre configurações de projeto de migração, consulte [configurações do projeto (migração)](http://msdn.microsoft.com/en-us/fcd6b988-633b-4b2b-9f36-6368b5e86b60) .  
  
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
[Migração de dados Oracle para o SQL Server](http://msdn.microsoft.com/en-us/e23c5268-41ed-4e55-9fe7-a11376202a13)  
  
