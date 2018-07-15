---
title: Tratamento de erro | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: ff79e19d-afca-42a4-81b0-62d759380d11
caps.latest.revision: 10
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 0f2c47fee88ba536c084649669ac5cd5f53cf6d4
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37318816"
---
# <a name="error-handling"></a>Tratamento de erros
  Uma Instância do Oracle CDC mina as alterações de um único banco de dados de origem do Oracle (um cluster do Oracle RAC é considerado um banco de dados único) e grava as alterações confirmadas em tabelas de alteração em um banco de dados do CDC na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino.  
  
 Uma Instância CDC mantém seu estado em uma tabela do sistema chamada **cdc.xdbcdc_state**. Esta tabela pode ser consultada a qualquer hora para localizar o estado da Instância CDC. Para obter mais informações sobre a tabela cdc.xdbcdc_state, consulte [cdc.xdbcdc_state](the-oracle-cdc-databases.md#BKMK_cdcxdbcdc_state).  
  
 A tabela a seguir descreve os estados da Instância CDC na tabela xdbcdc_state.  
  
 Para cada estado, as duas indicações a seguir são mostradas para as colunas correspondentes na tabela cdc.xdbcdc_state:  
  
-   A instância não está ativa (não há nenhum processo do Windows tratando isto no momento). Se o valor de coluna **ativo** for 1, um subprocesso do Serviço Oracle CDC que trata esta Instância Oracle CDC específica estará em execução.  
  
-   Se o valor de coluna de **erro** for 0, a Instância Oracle CDC não estará em uma condição de erro. Se o valor de coluna de **erro** for 1, haverá um erro que impede que a Instância Oracle CDC processe alterações.  
  
     Se a coluna de **erro** tiver um valor de 1 e o valor de coluna **ativo** também for 1, um erro recuperável estará ocorrendo para a Instância Oracle CDC que pode ser resolvida automaticamente. Se a coluna de erro tiver um valor de 1 e a coluna ativa tiver um valor de 0, na maioria dos casos, uma solução alternativa manual poderá ser necessária para resolver o problema antes que o processamento possa ser retomado.  
  
 A tabela a seguir descreve os vários códigos de status que a Instância Oracle CDC pode relatar em sua tabela de estado.  
  
|Status|Código de status ativo|Código do estado de erro|Descrições|  
|------------|------------------------|-----------------------|------------------|  
|ABORTED|0|1|A Instância do Oracle CDC não está sendo executada. O substatus ABORTED indica que a Instância Oracle CDC estava ACTIVE e foi parada inesperadamente.<br /><br /> O substatus ABORTED é estabelecido pela instância principal do Serviço Oracle CDC quando ela detectar que a Instância Oracle CDC não está sendo executada enquanto seu status estiver ACTIVE.|  
|erro|0|1|A Instância do Oracle CDC não está sendo executada. O status de ERROR indica que a instância de CDC estava ACTIVE, mas encontrou um erro que não é recuperável e foi desabilitada. O status de ERROR contém os códigos de substatus a seguir:<br /><br /> MISCONFIGURED: um erro de configuração irrecuperável foi detectado.<br /><br /> PASSWORD-REQUIRED: não há nenhuma senha definida para o Designer da Captura de Dados de Alteração para Oracle da Attunity ou a senha configurada não é válida. Isto pode ocorrer devido a uma alteração na senha da chave assimétrica do serviço.|  
|RUNNING|1|0|A instância CDC está sendo executada e está processando registros de alteração. O status RUNNING contém os seguintes códigos de substatus:<br /><br /> IDLE: Todos os registros de alteração foram processados e armazenados nas tabelas de controle de destino (**_CT**). Não há nenhuma transação ativa com as tabelas de controle.<br /><br /> PROCESSING: há registros de alteração sendo processados que ainda não estão gravados nas tabelas de controle (**_CT**).|  
|STOPPED|0|0|A instância CDC não está em execução. O substatus STOP indica que a instância CDC estava ACTIVE e foi parada corretamente.|  
|SUSPENDED|1|1|A instância de CDC está sendo executada, mas o processamento é suspenso devido a um erro recuperável. O status SUSPENDED contém os seguintes códigos de substatus:<br /><br /> DISCONNECTED: a conexão com o banco de dados Oracle de origem não pode ser estabelecida. O processamento será retomado assim que a conexão for restaurada.<br /><br /> STORAGE: o armazenamento está completo. O processamento será retomado quando o armazenamento estiver disponível. Em alguns casos, este status pode não aparecer porque a tabela de status não pode ser atualizada.<br /><br /> LOGGER: O registrador está conectado ao Oracle, mas não pode ler os logs de transação do Oracle devido a um problema temporário.|  
|DATAERROR|x|x|Este código de status só é usado para a tabela **xdbcdc_trace** . Ele não aparece na tabela **xdbcdc_state** . Os registros de rastreamento com este status indicam um problema com um registro de log da Oracle. O registro de log incorreto está armazenado na coluna **dados** como um BLOB. O status DATAERROR contém os códigos de substatus a seguir:<br /><br /> BADRECORD: o registro de log anexado não pôde ser analisado.<br /><br /> CONVERT-ERROR: os dados em algumas colunas não puderam ser convertidos nos dados das colunas de destino na tabela de captura. Este status somente poderá aparecer se a configuração especificar que os erros de conversão devem gerar registros de rastreamento.|  
  
 Como o estado do Serviço Oracle CDC está armazenado no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], pode haver casos em que o valor de estado no banco de dados pode não refletir o estado real do serviço. O cenário mais comum é quando o serviço perde sua conexão com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e não pode retomá-la (por qualquer motivo). Nesse caso, o estado armazenado em **cdc.xdbcdc_state** fica obsoleto. Se o último carimbo de data/hora de atualização (UTC) tiver mais de um minuto, o estado será provavelmente obsoleto. Neste caso, use o Visualizador de Eventos do Windows para localizar informações adicionais sobre o status do serviço.  
  
## <a name="error-handling"></a>Tratamento de erros  
 Esta seção descreve como o Serviço Oracle CDC trata erros.  
  
### <a name="logging"></a>Log  
 O Serviço Oracle CDC cria informações de erro em um dos locais a seguir.  
  
-   O log de eventos do Windows, que é usado para registrar erros e indicar os eventos de ciclo de vida do Serviço Oracle CDC (iniciando, parando, (re) conexão com a instância de destino do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ).  
  
-   A tabela MSXDBCDC.dbo.xdbcdc_trace, que é usada para registros gerais e rastreamento pelo processo principal do Serviço Oracle CDC.  
  
-   A tabela \<cdc-database>.cdc.xdbcdc_trace, que é usada para registros gerais e rastreamento pelas Instâncias Oracle CDC. Isto significa que os erros relacionados a uma Instância Oracle CDC específica são registrados em uma tabela de rastreamento daquela instância.  
  
 As informações são registradas em log pelo serviço Oracle CDC quando o serviço:  
  
-   É iniciado ou parado pelo gerenciador de controle de serviço.  
  
-   Não é possível conectar-se à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] associada e quando ele estabelece uma conexão bem-sucedida após uma falha.  
  
-   Encontra um erro que inicia as instâncias de Serviço Oracle CDC.  
  
-   Detecta que uma Instância Oracle CDC foi anulada.  
  
-   Encontra um erro inesperado.  
  
 As informações são registradas em log pela instância CDC quando a instância:  
  
-   Está habilitada ou desabilitada.  
  
-   Encontra um erro.  
  
-   Recupera-se de um erro recuperável.  
  
 A tabela de rastreamento também é usada para registrar informações de rastreamento detalhadas para solucionar problemas.  
  
### <a name="handling-source-oracle-connection-errors"></a>Tratando erros de conexão do Oracle de origem  
 O Serviço Oracle CDC precisa de uma conexão persistente com o banco de dados Oracle de origem. Muitos erros de conexão que não estão relacionados à configuração de serviço (como erros de sistema de rede) são considerados temporários. Portanto, se o Serviço Oracle CDC não puder estabelecer conexão com o banco de dados Oracle (ou no início ou durante o trabalho depois de uma desconexão), o serviço alterará seu estado para SUSPENDED/DISCONNECTED e inserirá um loop de repetição quando a conexão for tentada novamente em intervalos regulares. Quando a conexão for restabelecida, o processamento continuará.  
  
 Outros tipos de erros de conexão não são temporários (por exemplo, credenciais incorretas, privilégios insuficientes e endereço de banco de dados incorreto). Quando estes erros ocorrerem, o estado do Serviço Oracle CDC será definido como ERROR/MISCONFIGURED ou ERRO/PASSWORD-REQUIRED e o serviço será desabilitado. Quando o usuário corrigir o erro subjacente, a Instância Oracle CDC deve ser reabilitada manualmente para que o processamento seja retomado.  
  
 Quando não estiver claro se o erro é temporário, será melhor presumir isto.  
  
### <a name="handling-target-sql-server-connection-errors"></a>Tratando erros de conexão do SQL Server de destino  
 O Serviço Oracle CDC precisa de uma conexão persistente para a instância [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino. Esta conexão é usada para:  
  
-   Verifique se não há nenhum outro serviço de mesmo nome funcionando atualmente com esta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Verifique qual Instância Oracle CDC está habilitada ou desabilitada e inicie (ou pare) seu subprocesso.  
  
 Quando o serviço estabelece uma conexão com a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e verifica se é o único serviço Oracle CDC com este nome que está funcionando, ele pode verificar quais instâncias Oracle CDC estão habilitadas e iniciar os processos de manipulação (posteriormente o serviço para estes processos quando forem desabilitados). As instâncias Oracle CDC usam as suas conexões do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para trabalhar com o banco de dados CDC da instância Oracle CDC.  
  
 A maneira como os erros são tratados quando a conexão para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino falha depende se os erros são temporários.  
  
 Para erros não temporários conhecidos (como credenciais incorretas, privilégios insuficientes, informações de conexão incorretas), o serviço registra em log um erro no log de evento do Windows e para (ele não pode gravar na tabela de rastreamento porque ele não pode se conectar ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]). Neste caso, o usuário deve resolver o erro e reiniciar o serviço do Windows do Oracle CDC.  
  
 Para erros temporários e erros inesperados, a operação é repetida novamente várias vezes e, se a falha persistir por um período de tempo significativo, o Serviço CDC parará seus subprocessos de Instância CDC e voltará para sua tentativa de conexão inicial (dessa vez, um Serviço Oracle CDC em outro computador já pode ter tomado o controle do serviço CDC nomeado).  
  
### <a name="handling-target-sql-server-storage-full-errors"></a>Tratando erros completos de armazenamento do SQL Server de destino  
 Quando o Serviço Oracle CDC detecta que não pode inserir novos dados de alteração no banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC de destino, ele grava um aviso no log de eventos e tenta inserir um registro de rastreamento (embora isso possa falhar pela mesma razão). Ele então tenta novamente a operação em um intervalo específico até que tenha êxito.  
  
### <a name="handling-oracle-cdc-errors"></a>Manipulando erros do Oracle CDC  
 A Instância Oracle CDC lê o log de transação do Oracle e o processa. Se o processamento de CDC encontrar um erro, ele será relatado na tabela **cdc.xdbcdc_state** e o usuário precisará intervir manualmente com base no erro relatado.  
  
 Por exemplo, a Instância Oracle CDC não pode estar ativa para uma duração estendida e os logs de transação necessários do Oracle não estão mais disponíveis. Neste caso, o DBA do Oracle deverá restaurar os logs necessários para que a Instância Oracle CDC retome o processamento.  
  
### <a name="handling-unexpected-oracle-cdc-instance-failures"></a>Tratando falhas inesperadas da Instância Oracle CDC  
 O Serviço Oracle CDC monitora seus subprocessos de Instância CDC. Quando um subprocesso de Instância CDC é anulado, o Serviço CDC desabilita-o na tabela MSXDBCDC.dbo.xdbcdc_databases e atualiza seu status de cdc.xdbcdc_state para ABORTED. Neste caso, a caixa de diálogo padrão de Relatório de Erros do Windows é usada para relatar este erro para análise posterior.  
  
## <a name="see-also"></a>Consulte também  
 [Change Data Capture Designer para Oracle da attunity](change-data-capture-designer-for-oracle-by-attunity.md)   
 [A instância Oracle CDC](the-oracle-cdc-instance.md)  
  
  
