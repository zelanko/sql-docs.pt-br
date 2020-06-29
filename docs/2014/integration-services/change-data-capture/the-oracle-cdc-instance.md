---
title: A Instância Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: ed71e8c4-e013-4bf2-8b6c-1e833ff2a41d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: a9f4b99c65ef2a3927ee31380e7931209830841a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85435263"
---
# <a name="the-oracle-cdc-instance"></a>A instância Oracle CDC
  A Instância Oracle CDC é um processo criado pelo Serviço Oracle CDC para processar alterações capturadas de um único banco de dados de origem Oracle. A Instância Oracle CDC recupera sua configuração da tabela **cdc.xdbcdc_config** e mantém seu estado na tabela **cdc.xdbcdc_state** . Estas tabelas fazem parte do banco de dados CDC, que define a Instância Oracle CDC. Para obter mais informações sobre o banco de dados e as tabelas xdbcdc, consulte [The CDC Databases](the-oracle-cdc-service.md).  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tratamento de erro](error-handling.md)  
  
  
