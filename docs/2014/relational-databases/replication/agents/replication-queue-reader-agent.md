---
title: Agente de Leitor de Fila de Replicação | Microsoft Docs
ms.custom: ''
ms.date: 10/29/2018
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: replication
ms.topic: conceptual
helpviewer_keywords:
- agents [SQL Server replication], Queue Reader Agent
- command prompt [SQL Server replication]
- Queue Reader Agent, parameter reference
- Queue Reader Agent, executables
ms.assetid: 8e227793-11f6-47c6-99dc-ffc282f5d4bf
author: MashaMSFT
ms.author: mathoma
manager: craigg
ms.openlocfilehash: d92a15ae855c5521319abd252b1f5a7efc2bf300
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63191667"
---
# <a name="replication-queue-reader-agent"></a>Agente de Leitor de Fila de Replicação
  O Queue Reader Agent de replicação é um executável que lê as mensagens armazenadas [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em uma fila [!INCLUDE[msCoName](../../../includes/msconame-md.md)] ou uma fila de mensagens e, em seguida, aplica essas mensagens ao Publicador. O Queue Reader Agent é usado com publicações de instantâneo e transacionais que permitem atualização em fila.  
  
> [!NOTE]  
>  Os parâmetros podem ser especificados em qualquer ordem. Quando não são especificados parâmetros opcionais, são usados valores predefinidos com base no perfil de agente padrão.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      qrdrsvc [-?]  
[-Continuous]  
[-DefinitionFiledefinition_file]  
[-Distributorserver_name[\instance_name]]  
[-DistributionDBdistribution_database]  
[-DistributorLogindistributor_login]  
[-DistributorPassworddistributor_password]  
[-DistributorSecurityMode [0|1]]  
[-EncryptionLevel [0|1|2]]  
[-HistoryVerboseLevel [0|1|2|3]]  
[-LoginTimeOutlogin_time_out_seconds]  
[-Outputoutput_path_and_file_name]  
[-OutputVerboseLevel [0|1|2]]  
[-PollingIntervalpolling_interval]  
[-PublisherFailoverPartnerserver_name[\instance_name] ]  
[-ProfileNameagent_profile_name]  
[-QueryTimeOutquery_time_out_seconds]  
[-ResolverState [1|2|3]]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-?**  
 Exibe informações de uso.  
  
 **-Contínuo**  
 Especifica se o agente tenta processar transações em fila continuamente. Se especificado, o agente continua a execução, mesmo que não haja transações na fila pendentes de nenhum dos assinantes.  
  
 **-Definitionfile** _def_path_and_file_name_  
 É o caminho do arquivo de definição de agente. Um arquivo de definição de agente contém argumentos de linha de comando para o agente. O conteúdo do arquivo é analisado como um arquivo executável. Use aspas duplas (") para especificar valores de argumentos que contêm caracteres arbitrários.  
  
 **-** _Server_name_do distribuidor**\\**[_instance_name_]  
 É o nome do Distribuidor. Especifique *server_name* para a instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] naquele servidor. Especifique *server_name*\\*instance_name* para uma instância nomeada do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] nesse servidor. Se não for especificado, o nome assumirá o padrão do nome da instância padrão do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] no computador local.  
  
 **-DistributionDB** _distribution_database_  
 É o banco de dados de distribuição.  
  
 **-DistributorLogin** _distributor_login_  
 É o nome de logon do Distribuidor.  
  
 **-DistributorPassword** _distributor_password_  
 É a senha do Distribuidor.  
  
 **-DistributorSecurityMode** [ **0**| **1**]  
 Especifica o modo de segurança do Distribuidor. Um valor de **0** indica [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] o modo de autenticação (padrão) e um valor de **1** indica o modo de autenticação do Windows.  
  
 **-EncryptionLevel** [ **0** | **1** | **2** ]  
 É o nível da criptografia SSL (Secure Sockets Layer) usada pelo Queue Reader Agent ao fazer conexões.  
  
|Valor EncryptionLevel|DESCRIÇÃO|  
|---------------------------|-----------------|  
|**0**|Especifica que o SSL não é usado.|  
|**1**|Especifica que o SSL é usado, mas que +o agente não verifica se o certificado de servidor SSL é assinado por um emissor confiável.|  
|**2**|Especifica que o SSL é usado, e que o certificado é verificado.|  

 > [!NOTE]  
 >  É definido um certificado SSL válido com um nome de domínio totalmente qualificado do SQL Server. Para que o agente seja conectado com êxito ao definir -EncryptionLevel como 2, crie um alias no SQL Server local. O parâmetro 'Alias Name' deve ser o nome do servidor e o parâmetro 'Server' deve ser definido como o nome totalmente qualificado do SQL Server.
  
 Para obter mais informações, consulte [replicação do SQL Server Security](../security/view-and-modify-replication-security-settings.md).  
  
 **-HistoryVerboseLevel** [ **0**| **1**| **2**| **3**]  
 Especifica a quantidade de histórico registrada durante uma operação de leitura de fila. Você pode minimizar o efeito de registro de histórico no desempenho selecionando **1**.  
  
|Valor HistoryVerboseLevel|DESCRIÇÃO|  
|-------------------------------|-----------------|  
|**0**|Nenhum log de histórico (não recomendado).|  
|**1**|Padrão. Sempre atualiza uma mensagem de histórico anterior do mesmo status (inicialização, andamento, êxito, etc.). Se nenhum registro anterior com o mesmo status existir, insira um registro novo.|  
|**2**|Insira novos registros de histórico, incluindo mensagens ociosas ou mensagens de trabalho de execução longa.|  
|**Beta**|Insira novos registros de histórico que incluam detalhes adicionais que podem ser úteis na solução de problemas.|  
  
 **-LoginTimeOut** _login_time_out_seconds_  
 É o número de segundos antes que o logon expire. O padrão é 15 segundos.  
  
 **-Saída** _output_path_and_file_name_  
 É o caminho do arquivo de saída do agente. Se o nome de arquivo não for fornecido, a saída será enviada ao console. Se o nome do arquivo especificado existir, a saída será anexada ao arquivo.  
  
 **-OutputVerboseLevel** [ **0**| **1**| **2**]  
 Especifica se a saída deve ser detalhada. Se o nível detalhado for **0**, só mensagens de erro serão impressas. Se o nível detalhado for **1**, todas as mensagens de relatório de progresso serão impressas. Se o nível detalhado for **2** (padrão), todas as mensagens de erro e de relatório de progresso serão impressas, o que é útil na depuração.  
  
 **-PollingInterval** _polling_interval_  
 É relevante apenas para assinaturas de atualização que usam filas com base no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . Especifica com que frequência, em segundos, a fila do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] é sondada para transações em fila pendentes. O valor pode ser entre 0 e 240 segundos. O padrão é 5 segundos.  
  
 **-PublisherFailoverPartner** _server_name_[**\\**_instance_name_]  
 Especifica a instância de parceiro de failover do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que participa de uma sessão de espelhamento de banco de dados com o banco de dados de publicação. Para obter mais informações, consulte [Espelhamento e replicação de banco de dados &#40;SQL Server&#41;](../../../database-engine/database-mirroring/database-mirroring-and-replication-sql-server.md).  
  
 **-Profilename** _agent_profile_name_  
 É o nome de um perfil de agente usado para fornecer um conjunto de valores padrão ao agente. Para obter mais informações, consulte [Perfis do agente de replicação](replication-agent-profiles.md).  
  
 **-QueryTimeOut** _query_time_out_seconds_  
 É o número de segundos antes que a consulta expire. O padrão é 1800 segundos.  
  
 **-Resolvedor** [ **1**| **2**| **3**]  
 Especifica como conflitos de atualização na fila são resolvidos. Um valor **1** indica que o Publicador ganha o conflito, a transação na fila conflitante será revertida no Publicador e no Assinante de atualização de origem e o processo de transações subsequentes em fila continuará. Um valor **2** indica que o Assinante ganha o conflito e a transação na fila substituirá os valores no Publicador. Um valor **3** indica que qualquer conflito resultará na reinicialização do Assinante; o Publicador ganha o conflito, o processamento de transações subsequentes na fila será interrompido e a assinatura será reiniciada. A configuração padrão é **1** para publicações transacionais e **3** para publicações de instantâneo.  
  
## <a name="remarks"></a>Comentários  
 Para iniciar o Queue Reader Agent, execute **qrdrsvc.exe** no prompt de comando. Para obter informações, consulte [Executáveis do agente de replicação](../concepts/replication-agent-executables-concepts.md).  
  
## <a name="see-also"></a>Consulte Também  
 [Administração do agente de replicação](replication-agent-administration.md)  
  
  
