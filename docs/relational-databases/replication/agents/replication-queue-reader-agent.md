---
title: "Replication Queue Reader Agent | Microsoft Docs"
ms.custom: ""
ms.date: "06/02/2016"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "replication"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "agentes [replicação do SQL Server], Queue Reader Agent"
  - "prompt de comando [replicação do SQL Server]"
  - "Queue Reader Agent, referência de parâmetro"
  - "Queue Reader Agent, executáveis"
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
caps.latest.revision: 36
author: "BYHAM"
ms.author: "rickbyh"
manager: "jhubbard"
caps.handback.revision: 36
---
# Replication Queue Reader Agent
  O Replication Queue Reader Agent é um executável que lê mensagens armazenadas em uma [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] fila ou um [!INCLUDE[msCoName](../../../includes/msconame-md.md)] fila de mensagens e, em seguida, aplica essas mensagens no publicador. O Queue Reader Agent é usado com publicações de instantâneo e transacionais que permitem atualização em fila.  
  
> [!NOTE]  
>  Os parâmetros podem ser especificados em qualquer ordem. Quando não são especificados parâmetros opcionais, são usados valores predefinidos com base no perfil de agente padrão.  
  
## Sintaxe  
  
```  
  
qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFile definition_file]  
[-Distributor server_name[\instance_name]]  
[-DistributionDB distribution_database]  
[-DistributorLogin distributor_login]  
[-DistributorPassword distributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOut login_time_out_seconds]  
[-Output output_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingInterval polling_interval]  
[-PublisherFailoverPartner server_name[\instance_name] ]  
[-ProfileName agent_profile_name]  
[-QueryTimeOut query_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## Argumentos  
 **-?**  
 Exibe informações de uso.  
  
 **-Continuous**  
 Especifica se o agente tenta processar transações em fila continuamente. Se especificado, o agente continua a execução, mesmo que não haja transações na fila pendentes de nenhum dos assinantes.  
  
 **-DefinitionFile** *def_path_and_file_name*  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de linha de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar valores de argumentos que contêm caracteres arbitrários.  
  
 **-Distribuidor** *nome_do_servidor*[**\\***instance_name*]  
 É o nome do Distribuidor. Especifique *nome_do_servidor* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Especifique *nome_do_servidor*\\*nome_da_instância* para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Se não for especificado, o nome assumirá o padrão do nome da instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no computador local.  
  
 **-DistributionDB** *distribution_database*  
 É o banco de dados de distribuição.  
  
 **Parâmetros - DistributorLogin** *distributor_login*  
 É o nome de logon do Distribuidor.  
  
 **-DistributorPassword** *distributor_password*  
 É a senha do Distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor de **0** indica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] modo de autenticação (padrão) e um valor de **1** indica o modo de autenticação do Windows.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível da criptografia SSL (Secure Sockets Layer) usada pelo Queue Reader Agent ao fazer conexões.  
  
|Valor EncryptionLevel|Descrição|  
|---------------------------|-----------------|  
|**0**|Especifica que o SSL não é usado.|  
|**1**|Especifica que o SSL é usado, mas que +o agente não verifica se o certificado de servidor SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o SSL é usado, e que o certificado é verificado.|  
  
 Para obter mais informações, consulte [Visão geral de segurança e 40; Replicação e 41;](../../../relational-databases/replication/security/security-overview-replication.md).  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 Especifica a quantidade de histórico registrada durante uma operação de leitura de fila. Você pode minimizar o efeito de registro de histórico no desempenho selecionando **1**.  
  
|Valor HistoryVerboseLevel|Descrição|  
|-------------------------------|-----------------|  
|**0**|Nenhum log de histórico (não recomendado).|  
|**1**|Padrão. Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2**|Insira novos registros de histórico, incluindo mensagens ociosas ou mensagens de trabalho de execução longa.|  
|**3**|Insira novos registros de histórico que incluam detalhes adicionais que podem ser úteis na solução de problemas.|  
  
 **-LoginTimeOut** *login_time_out_seconds*  
 É o número de segundos antes que o logon expire. O padrão é 15 segundos.  
  
 **-Saída** *output_path_and_file_name*  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica se a saída deve ser detalhada. Se o nível detalhado for **0**, só mensagens de erro serão impressas. Se o nível detalhado for **1**, todas as mensagens de relatório de progresso serão impressas. Se o nível detalhado for **2** (padrão), todas as mensagens de erro e mensagens de relatório de progresso são impressas, que é útil para depuração.  
  
 **-PollingInterval** *polling_interval*  
 É relevante apenas para assinaturas de atualização que usam filas com base no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Especifica com que frequência, em segundos, a fila do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é sondada para transações em fila pendentes. O valor pode ser entre 0 e 240 segundos. O padrão é 5 segundos.  
  
 **-PublisherFailoverPartner** *nome_do_servidor*[**\\***instance_name*]  
 Especifica a instância de parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa de uma sessão de espelhamento de banco de dados com o banco de dados de publicação. Para obter mais informações, consulte [espelhamento de banco de dados, replicação e 40; SQL Server & 41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-ProfileName** *agent_profile_name*  
 É o nome de um perfil de agente usado para fornecer um conjunto de valores padrão ao agente. Para obter informações, consulte [perfis do Replication Agent](../../../relational-databases/replication/agents/replication-agent-profiles.md).  
  
 **-QueryTimeOut** *query_time_out_seconds*  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-ResolverState** [ **1**| **2**| **3**]  
 Especifica como conflitos de atualização na fila são resolvidos. Um valor de **1** indica o publicador vence o conflito e conflitantes na fila de transação será revertida no publicador e o assinante de atualização de origem; continuará o processamento de transações subsequentes na fila atual. Um valor de **2** indica que o assinante vence o conflito e a transação na fila substituirá os valores no Editor. Um valor de **3** indica que qualquer conflito resultará na reinicialização do assinante; o publicador vence o conflito, processamento de transações subsequentes na fila será encerrado e a assinatura será reiniciada. A configuração padrão é **1** para publicações transacionais e **3** para publicações de instantâneo.  
  
## Comentários  
 Para iniciar o Queue Reader Agent, execute **qrdrsvc.exe** no prompt de comando. Para obter informações, consulte [Executáveis do agente de replicação](../../../relational-databases/replication/concepts/replication-agent-executables-concepts.md).  
  
## Consulte também  
 [Administração do agente de replicação](../../../relational-databases/replication/agents/replication-agent-administration.md)  
  
  