---
title: Colunas de dados de relatórios de andamento | Microsoft Docs
ms.date: 05/07/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: tabular-models
ms.topic: reference
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7d8dd07cbaf7ca4b9942b09f0f538a14a883e694
ms.sourcegitcommit: 1aedef909f91dc88dc741748f36eabce3a04b2b1
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/08/2018
---
# <a name="progress-reports-data-columns"></a>Colunas de dados de relatórios de andamento
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  A categoria de evento Progress Reports tem as seguintes classes de evento:  
  
|**ID do evento**|**Nome do evento**|**Descrição do evento**|  
|------------------|--------------------|---------------------------|  
|5|Progress Report Begin|Progress report begin.|  
|6|Progress Report End|Progress report end.|  
|7|Progress Report Current|Relatório de andamento atual.|  
|8|Progress Report Error|Erro do relatório de andamento.|  
  
 As tabelas a seguir listam as colunas de dados de cada uma dessas classes de evento.  
  
## <a name="progress-report-begindata-columns"></a>Progress Report Begin - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. A seguir, estão os pares **ID da Subclasse**: **Nome da Subclasse** válidos:<br /><br /> 1: **Processar**<br /><br /> 2: **Mesclar**<br /><br /> 3: **Excluir**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Recriar**<br /><br /> 6: **Confirmar**<br /><br /> 7: **Reverter**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transação**<br /><br /> 12: **Inicializar**<br /><br /> 13: **Discretizar**<br /><br /> 14: **Consultar**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Agregar**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Conectando**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restaurar**<br /><br /> 39: **Sincronizar**<br /><br /> 40: **Criar Agendamento de Processamento**<br /><br /> 41: **Desanexar**<br /><br /> 42: **Anexar**<br /><br /> 43: **Analisar\Codificar Dados**<br /><br /> 44: **Compactar Segmento**<br /><br /> 45: **Gravar Coluna da Tabela**<br /><br /> 46: **Preparar Compilação da Relação**<br /><br /> 47: **Criar Segmento da Relação**<br /><br /> 48: **Carregar**<br /><br /> 49: **Carregar Metadados**<br /><br /> 50: **Carregar Dados**<br /><br /> 51: **Carregar Postagem**<br /><br /> 52: **Passagem de Metadados durante Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Processamento da hierarquia**<br /><br /> 55: **Alternância de dicionário**|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|Contém a ID de trabalho associada ao evento relatado.|  
|SessionType|8|8|Contém o tipo de sessão (a entidade que causa o evento) associado ao evento relatado. Para o processamento de eventos, os valores são:<br /><br /> 1 = Usuário<br /><br /> 2 = Cache pró-ativo<br /><br /> 3= Processamento lento|  
|ObjectID|11|8|Contém a ID de objeto (uma cadeia de caracteres) associada ao evento relatado.|  
|ObjectType|12|1|Contém o tipo de objeto.|  
|ObjectName|13|8|Contém o nome do objeto associado ao evento relatado.|  
|ObjectPath|14|8|Contém o caminho do objeto associado ao evento relatado, como uma lista de pais separados por vírgula, começando com os pais do objeto.|  
|ObjectReference|15|8|Contém a referência de objeto para o evento relatado, codificada como XML para todos os pais e usando marcas para descrever o objeto.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento relatado.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento relatado ocorreu.|  
|NTUserName|32|8|Contém a conta de usuário do Windows associada ao evento relatado.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento relatado.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento relatado.|  
|NTCanonicalUserName|40|8|Nome do usuário na forma canônica. Por exemplo, engineering.microsoft.com/software/someone.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento relatado. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|TextData|42|9|Contém os dados de texto associados ao evento relatado.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que o evento relatado ocorreu.|  
  
## <a name="progress-report-enddata-columns"></a>Progress Report End - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. A seguir, estão os pares **ID da Subclasse**: **Nome da Subclasse** válidos:<br /><br /> 1: **Processar**<br /><br /> 2: **Mesclar**<br /><br /> 3: **Excluir**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Recriar**<br /><br /> 6: **Confirmar**<br /><br /> 7: **Reverter**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transação**<br /><br /> 12: **Inicializar**<br /><br /> 13: **Discretizar**<br /><br /> 14: **Consultar**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Agregar**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Conectando**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restaurar**<br /><br /> 39: **Sincronizar**<br /><br /> 40: **Criar Agendamento de Processamento**<br /><br /> 41: **Desanexar**<br /><br /> 42: **Anexar**<br /><br /> 43: **Analisar\Codificar Dados**<br /><br /> 44: **Compactar Segmento**<br /><br /> 45: **Gravar Coluna da Tabela**<br /><br /> 46: **Preparar Compilação da Relação**<br /><br /> 47: **Criar Segmento da Relação**<br /><br /> 48: **Carregar**<br /><br /> 49: **Carregar Metadados**<br /><br /> 50: **Carregar Dados**<br /><br /> 51: **Carregar Postagem**<br /><br /> 52: **Passagem de Metadados durante Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Processamento da hierarquia**<br /><br /> 55: **Alternância de dicionário**|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Contém o tempo decorrido (em milissegundos) utilizado pelo evento.|  
|CPUTime|6|2|Contém a quantidade de tempo da CPU (em milissegundos) usado pelo evento.|  
|JobID|7|1|Contém a ID de trabalho associada ao evento relatado.|  
|SessionType|8|8|Contém o tipo de sessão (a entidade que causa o evento) associado ao evento relatado. Para o processamento de eventos, os valores são:<br /><br /> 1 = Usuário<br /><br /> 2 = Cache pró-ativo<br /><br /> 3= Processamento lento|  
|ProgressTotal|9|1|Contém o total de andamento do evento relatado.|  
|IntegerData|10|1|Contém os dados inteiros associados ao evento relatado, como a contagem atual do número de linhas processadas para um evento de processamento.|  
|ObjectID|11|8|Contém a ID de objeto (uma cadeia de caracteres) associada ao evento relatado.|  
|ObjectType|12|1|Contém o tipo de objeto.|  
|ObjectName|13|8|Contém o nome do objeto associado ao evento relatado.|  
|ObjectPath|14|8|Contém o caminho do objeto associado ao evento relatado, como uma lista de pais separados por vírgula, começando com os pais do objeto.|  
|ObjectReference|15|8|Contém a referência de objeto para o evento relatado, codificada como XML para todos os pais e usando marcas para descrever o objeto.|  
|Severity|22|1|Contém o nível de severidade de uma exceção associada ao evento relatado. Os valores são:<br /><br /> 0 = Êxito<br /><br /> 1 = Informativo<br /><br /> 2 = Aviso<br /><br /> 3 = Erro|  
|Success|23|1|Contém o êxito ou a falha do evento relatado do servidor. Os valores são:<br /><br /> 0 = Falha<br /><br /> 1 = Êxito|  
|Erro|24|1|Contém o número do erro de determinado evento.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento relatado.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento relatado ocorreu.|  
|NTUserName|32|8|Contém a conta de usuário do Windows associada ao evento relatado.|  
|NTDomainName|33|8|Contém a conta de domínio do Windows associada ao evento relatado.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento relatado.|  
|NTCanonicalUserName|40|8|Contém o nome de usuário do Windows associado ao evento relatado. O nome de usuário está na forma canônica. Por exemplo, engineering.microsoft.com/software/user.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento relatado. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|TextData|42|9|Contém os dados de texto associados ao evento relatado.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que o evento relatado ocorreu.|  
  
## <a name="progress-report-currentdata-columns"></a>Progress Report Current - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. A seguir, estão os pares **ID da Subclasse**: **Nome da Subclasse** válidos:<br /><br /> 1: **Processar**<br /><br /> 2: **Mesclar**<br /><br /> 3: **Excluir**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Recriar**<br /><br /> 6: **Confirmar**<br /><br /> 7: **Reverter**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transação**<br /><br /> 12: **Inicializar**<br /><br /> 13: **Discretizar**<br /><br /> 14: **Consultar**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Agregar**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Conectando**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restaurar**<br /><br /> 39: **Sincronizar**<br /><br /> 40: **Criar Agendamento de Processamento**<br /><br /> 41: **Desanexar**<br /><br /> 42: **Anexar**<br /><br /> 43: **Analisar\Codificar Dados**<br /><br /> 44: **Compactar Segmento**<br /><br /> 45: **Gravar Coluna da Tabela**<br /><br /> 46: **Preparar Compilação da Relação**<br /><br /> 47: **Criar Segmento da Relação**<br /><br /> 48: **Carregar**<br /><br /> 49: **Carregar Metadados**<br /><br /> 50: **Carregar Dados**<br /><br /> 51: **Carregar Postagem**<br /><br /> 52: **Passagem de Metadados durante Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Processamento da hierarquia**<br /><br /> 55: **Alternância de dicionário**|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|JobID|7|1|Contém a ID de trabalho associada ao evento relatado.|  
|SessionType|8|8|Contém o tipo de sessão (a entidade que causa o evento) associado ao evento relatado. Para o processamento de eventos, os valores são:<br /><br /> 1 = Usuário<br /><br /> 2 = Cache pró-ativo<br /><br /> 3= Processamento lento|  
|ProgressTotal|9|1|Contém o total de andamento do evento relatado.|  
|IntegerData|10|1|Contém os dados inteiros associados ao evento relatado, como a contagem atual do número de linhas processadas para um evento de processamento.|  
|ObjectID|11|8|Contém a ID de objeto (uma cadeia de caracteres) associada ao evento relatado.|  
|ObjectType|12|1|Contém o tipo de objeto.|  
|ObjectName|13|8|Contém o nome do objeto associado ao evento relatado.|  
|ObjectPath|14|8|Contém o caminho do objeto associado ao evento relatado, como uma lista de pais separados por vírgula, começando com os pais do objeto.|  
|ObjectReference|15|8|Contém a referência de objeto para o evento relatado, codificada como XML para todos os pais e usando marcas para descrever o objeto.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento relatado.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento relatado ocorreu.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento relatado.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento relatado. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|TextData|42|9|Contém os dados de texto associados ao evento relatado.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que o evento relatado ocorreu.|  
  
## <a name="progress-report-errordata-columns"></a>Progress Report Error - Colunas de dados  
  
|**Nome da coluna**|**Id da coluna**|**Tipo de coluna**|**Descrição da coluna**|  
|---------------------|-------------------|---------------------|----------------------------|  
|EventClass|0|1|A classe de evento é usada para categorizar eventos.|  
|EventSubclass|1|1|A subclasse de evento oferece informações adicionais sobre cada classe de evento. A seguir, estão os pares **ID da Subclasse**: **Nome da Subclasse** válidos:<br /><br /> 1: **Processar**<br /><br /> 2: **Mesclar**<br /><br /> 3: **Excluir**<br /><br /> 4: **DeleteOldAggregations**<br /><br /> 5: **Recriar**<br /><br /> 6: **Confirmar**<br /><br /> 7: **Reverter**<br /><br /> 8: **CreateIndexes**<br /><br /> 9: **CreateTable**<br /><br /> 10: **InsertInto**<br /><br /> 11: **Transação**<br /><br /> 12: **Inicializar**<br /><br /> 13: **Discretizar**<br /><br /> 14: **Consultar**<br /><br /> 15: **CreateView**<br /><br /> 16: **WriteData**<br /><br /> 17: **ReadData**<br /><br /> 18: **GroupData**<br /><br /> 19: **GroupDataRecord**<br /><br /> 20: **BuildIndex**<br /><br /> 21: **Agregar**<br /><br /> 22: **BuildDecode**<br /><br /> 23: **WriteDecode**<br /><br /> 24: **BuildDMDecode**<br /><br /> 25: **ExecuteSQL**<br /><br /> 26: **ExecuteModifiedSQL**<br /><br /> 27: **Conectando**<br /><br /> 28: **BuildAggsAndIndexes**<br /><br /> 29: **MergeAggsOnDisk**<br /><br /> 30: **BuildIndexForRigidAggs**<br /><br /> 31: **BuildIndexForFlexibleAggs**<br /><br /> 32: **WriteAggsAndIndexes**<br /><br /> 33: **WriteSegment**<br /><br /> 34: **DataMiningProgress**<br /><br /> 35: **ReadBufferFullReport**<br /><br /> 36: **ProactiveCacheConversion**<br /><br /> 37: **Backup**<br /><br /> 38: **Restaurar**<br /><br /> 39: **Sincronizar**<br /><br /> 40: **Criar Agendamento de Processamento**<br /><br /> 41: **Desanexar**<br /><br /> 42: **Anexar**<br /><br /> 43: **Analisar\Codificar Dados**<br /><br /> 44: **Compactar Segmento**<br /><br /> 45: **Gravar Coluna da Tabela**<br /><br /> 46: **Preparar Compilação da Relação**<br /><br /> 47: **Criar Segmento da Relação**<br /><br /> 48: **Carregar**<br /><br /> 49: **Carregar Metadados**<br /><br /> 50: **Carregar Dados**<br /><br /> 51: **Carregar Postagem**<br /><br /> 52: **Passagem de Metadados durante Backup**<br /><br /> 53: **VertiPaq**<br /><br /> 54: **Processamento da hierarquia**<br /><br /> 55: **Alternância de dicionário**|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duration|5|2|Contém o tempo decorrido (em milissegundos) utilizado pelo evento.|  
|JobID|7|1|Contém a ID de trabalho associada ao evento relatado.|  
|SessionType|8|8|Contém o tipo de sessão (a entidade que causa o evento) associado ao evento relatado. Para o processamento de eventos, os valores são:<br /><br /> 1 = Usuário<br /><br /> 2 = Cache pró-ativo<br /><br /> 3= Processamento lento|  
|ProgressTotal|9|1|Contém o total de andamento do evento relatado.|  
|IntegerData|10|1|Contém os dados inteiros associados ao evento relatado, como a contagem atual do número de linhas processadas para um evento de processamento.|  
|ObjectID|11|8|Contém a ID de objeto (uma cadeia de caracteres) associada ao evento relatado.|  
|ObjectType|12|1|Contém o tipo de objeto.|  
|ObjectName|13|8|Contém o nome do objeto associado ao evento relatado.|  
|ObjectPath|14|8|Contém o caminho do objeto associado ao evento relatado, como uma lista de pais separados por vírgula, começando com os pais do objeto.|  
|ObjectReference|15|8|Contém a referência de objeto para o evento relatado, codificada como XML para todos os pais e usando marcas para descrever o objeto.|  
|Severity|22|1|Contém o nível de severidade de uma exceção associada ao evento relatado. Os valores são:<br /><br /> 0 = Êxito<br /><br /> 1 = Informativo<br /><br /> 2 = Aviso<br /><br /> 3 = Erro|  
|Erro|24|1|Contém o número do erro de determinado evento.|  
|ConnectionID|25|1|Contém a ID de conexão exclusiva associada ao evento relatado.|  
|DatabaseName|28|8|Contém o nome do banco de dados no qual o evento relatado ocorreu.|  
|SessionID|39|8|Contém a ID de sessão associada ao evento relatado.|  
|SPID|41|1|Contém a identificação do processo do servidor (SPID) que identifica de modo exclusivo a sessão de usuário associada ao evento relatado. A SPID corresponde diretamente à GUID de sessão usada pelo XML for Analysis (XMLA).|  
|TextData|42|9|Contém os dados de texto associados ao evento relatado.|  
|ServerName|43|8|Contém o nome da instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] em que o evento relatado ocorreu.|  
  
## <a name="see-also"></a>Consulte também  
 [Categoria de evento de relatórios de andamento](../../analysis-services/trace-events/progress-reports-event-category.md)  
  
  
