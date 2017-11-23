---
title: "A instância Oracle CDC | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: change-data-capture
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
caps.latest.revision: 8
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 13704cfef54e3401d31eb22f6dca9c9f247c079b
ms.contentlocale: pt-br
ms.lasthandoff: 08/03/2017

---
# <a name="the-oracle-cdc-instance"></a>A instância Oracle CDC
  A Instância Oracle CDC é um processo criado pelo Serviço Oracle CDC para processar alterações capturadas de um único banco de dados de origem Oracle. A Instância Oracle CDC recupera sua configuração da tabela **cdc.xdbcdc_config** e mantém seu estado na tabela **cdc.xdbcdc_state** . Estas tabelas fazem parte do banco de dados CDC, que define a Instância Oracle CDC. Para obter mais informações sobre o banco de dados e as tabelas xdbcdc, consulte [The CDC Databases](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md#BKMK_CDCdatabase).  
  
 Veja a seguir a descrição das tarefas realizadas pela instância Oracle CDC:  
  
-   **Tratando verificação de inicialização de serviço**: quando iniciado, a instância CDC carrega sua configuração da tabela **xdbcdc_config** e executa uma série de verificações de status que garantem que o estado persistido da instância CDC seja consistente e que possa iniciar alterações de processamento.  
  
-   **Preparando para captura de alterações**: quando a verificação for passada com êxito, a Instância Oracle CDC examinará todas as instâncias de captura definidas no momento e preparará as consultas do Oracle LogMiner e outras estruturas de suporte necessárias para a captura de alterações. Além disso, a instância Oracle recarrega o estado de captura interno que foi salvo da última vez que a Instância Oracle CDC foi executada.  
  
-   **Capturando alterações do Oracle**: a Instância Oracle CDC agrupa as alterações do Oracle por meio da facilidade Oracle LogMiner, ordena-as de acordo com a confirmação de transação e, em seguida, altera a hora em uma transação e grava-as nas tabelas de alteração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no banco de dados CDC.  
  
-   **Tratando o desligamento de serviço**: o ciclo de vida da Instância Oracle CDC é gerenciado pelo Serviço Oracle CDC. Quando a Instância Oracle CDC é solicitada para desligar, ela executa as tarefas a seguir:  
  
    -   Para de ler do log de transação do Oracle.  
  
    -   Para a gravação de transações do Oracle concluídas no banco de dados CDC.  
  
    -   Espera até 30 segundos (se necessário) até que a transação atual termine de gravar no banco de dados CDC. Se mais de 30 segundos se passarem, a gravação será cancelada e a transação será revertida (para ser tentada novamente quando a instância CDC for reiniciada).  
  
    -   Em um thread separado, grava o maior número de registros armazenados em cache de memória possível na tabela de transações preparadas por até 30 segundos (da transação mais antiga para a mais nova) e, em seguida, atualiza a tabela **xdbcdc_state** e confirma todas as alterações.  
  
-   **Tratando alterações de configuração**: a Instância Oracle CDC é notificada sobre as alterações de configuração pelo Serviço CDC ou detectando uma nova versão na tabela **cdc.xdbcdc_config** . A maioria das alterações não exige a reinicialização da Instância Oracle CDC (por exemplo, adicionar ou remover instâncias de captura). Porém, algumas alterações, como alterar a cadeia de conexão do Oracle ou credenciais de acesso, exigem a reinicialização da Instância CDC.  
  
-   **Tratando recuperação**: quando uma Instância Oracle CDC inicia, seu estado interno é restaurado das tabelas **xdbcdc_state** e **xdbcdc_staged_transactions** . Quando o estado é restaurado, a instância CDC continua como sempre.  
  
## <a name="see-also"></a>Consulte também  
 [Tratamento de erros](../../integration-services/change-data-capture/error-handling.md)  
  
  

