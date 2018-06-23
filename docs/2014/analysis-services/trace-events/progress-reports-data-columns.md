---
title: Colunas de dados de relatórios de andamento | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- analysis-services
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- Progress Reports event category
ms.assetid: d34a6322-e26b-4454-b98f-32307d6956b5
caps.latest.revision: 33
author: Minewiskan
ms.author: owend
manager: mblythe
ms.openlocfilehash: 8679a1e432402af28a36fa6ccfddac7f19fcf96c
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36116248"
---
# <a name="progress-reports-data-columns"></a>Colunas de dados de relatórios de andamento
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
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: processo<br /><br /> 2: mesclar<br /><br /> 3: excluir<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: recompile<br /><br /> 6: confirmar<br /><br /> 7: reversão<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transação<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: Criar modo de exibição<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregação<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar-se<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: backup<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: criar agendamento de processamento<br /><br /> 41: desanexar<br /><br /> 42: anexar<br /><br /> 43: analisar\codificar dados<br /><br /> 44: compactar segmento<br /><br /> 45: gravar coluna da tabela<br /><br /> 46: preparar compilação da relação<br /><br /> 47: criar segmento da relação<br /><br /> 48: carga<br /><br /> 49: carregar metadados<br /><br /> 50: carregamento de dados<br /><br /> 51: carregar postagem<br /><br /> 52: passagem de metadados durante Backup<br /><br /> 53: VertiPaq<br /><br /> 54: processamento da hierarquia<br /><br /> 55: alternância de dicionário|  
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
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: processo<br /><br /> 2: mesclar<br /><br /> 3: excluir<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: recompile<br /><br /> 6: confirmar<br /><br /> 7: reversão<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transação<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: Criar modo de exibição<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregação<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar-se<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: backup<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: criar agendamento de processamento<br /><br /> 41: desanexar<br /><br /> 42: anexar<br /><br /> 43: analisar\codificar dados<br /><br /> 44: compactar segmento<br /><br /> 45: gravar coluna da tabela<br /><br /> 46: preparar compilação da relação<br /><br /> 47: criar segmento da relação<br /><br /> 48: carga<br /><br /> 49: carregar metadados<br /><br /> 50: carregamento de dados<br /><br /> 51: carregar postagem<br /><br /> 52: passagem de metadados durante Backup<br /><br /> 53: VertiPaq<br /><br /> 54: processamento da hierarquia<br /><br /> 55: alternância de dicionário|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Contém o tempo decorrido (em milissegundos) utilizado pelo evento.|  
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
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: processo<br /><br /> 2: mesclar<br /><br /> 3: excluir<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: recompile<br /><br /> 6: confirmar<br /><br /> 7: reversão<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transação<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: Criar modo de exibição<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregação<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar-se<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: backup<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: criar agendamento de processamento<br /><br /> 41: desanexar<br /><br /> 42: anexar<br /><br /> 43: analisar\codificar dados<br /><br /> 44: compactar segmento<br /><br /> 45: gravar coluna da tabela<br /><br /> 46: preparar compilação da relação<br /><br /> 47: criar segmento da relação<br /><br /> 48: carga<br /><br /> 49: carregar metadados<br /><br /> 50: carregamento de dados<br /><br /> 51: carregar postagem<br /><br /> 52: passagem de metadados durante Backup<br /><br /> 53: VertiPaq<br /><br /> 54: processamento da hierarquia<br /><br /> 55: alternância de dicionário|  
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
|EventSubclass|1|1|A Subclasse de Evento oferece informações adicionais sobre cada classe de evento:<br /><br /> 1: processo<br /><br /> 2: mesclar<br /><br /> 3: excluir<br /><br /> 4: DeleteOldAggregations<br /><br /> 5: recompile<br /><br /> 6: confirmar<br /><br /> 7: reversão<br /><br /> 8: CreateIndexes<br /><br /> 9: CreateTable<br /><br /> 10: InsertInto<br /><br /> 11: transação<br /><br /> 12: inicializar<br /><br /> 13: discretizar<br /><br /> 14: consulta<br /><br /> 15: Criar modo de exibição<br /><br /> 16: WriteData<br /><br /> 17: ReadData<br /><br /> 18: GroupData<br /><br /> 19: GroupDataRecord<br /><br /> 20: BuildIndex<br /><br /> 21: agregação<br /><br /> 22: BuildDecode<br /><br /> 23: WriteDecode<br /><br /> 24: BuildDMDecode<br /><br /> 25: ExecuteSQL<br /><br /> 26: ExecuteModifiedSQL<br /><br /> 27: conectar-se<br /><br /> 28: BuildAggsAndIndexes<br /><br /> 29: MergeAggsOnDisk<br /><br /> 30: BuildIndexForRigidAggs<br /><br /> 31: BuildIndexForFlexibleAggs<br /><br /> 32: WriteAggsAndIndexes<br /><br /> 33: WriteSegment<br /><br /> 34: DataMiningProgress<br /><br /> 35: ReadBufferFullReport<br /><br /> 36: ProactiveCacheConversion<br /><br /> 37: backup<br /><br /> 38: restaurar<br /><br /> 39: sincronizar<br /><br /> 40: criar agendamento de processamento<br /><br /> 41: desanexar<br /><br /> 42: anexar<br /><br /> 43: analisar\codificar dados<br /><br /> 44: compactar segmento<br /><br /> 45: gravar coluna da tabela<br /><br /> 46: preparar compilação da relação<br /><br /> 47: criar segmento da relação<br /><br /> 48: carga<br /><br /> 49: carregar metadados<br /><br /> 50: carregamento de dados<br /><br /> 51: carregar postagem<br /><br /> 52: passagem de metadados durante Backup<br /><br /> 53: VertiPaq<br /><br /> 54: processamento da hierarquia<br /><br /> 55: alternância de dicionário|  
|CurrentTime|2|5|Contém a hora atual do evento relatado, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|StartTime|3|5|Contém a hora em que o evento iniciou, quando disponível. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|EndTime|4|5|Contém a hora em que o evento terminou. Esta coluna não é populada para classes de eventos iniciais, como SQL:BatchStarting ou SP:Starting. Para filtragem, os formatos esperados são 'AAAA-MM-DD' e 'AAAA-MM-DD HH:MM:SS'.|  
|Duração|5|2|Contém o tempo decorrido (em milissegundos) utilizado pelo evento.|  
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
 [Categoria de evento de Relatórios de andamento](progress-reports-event-category.md)  
  
  