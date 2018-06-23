---
title: Filtrar um rastreamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- filters [SQL Server], events
- events [SQL Server], filters
- filters [SQL Server]
- filters [SQL Server], traces
- traces [SQL Server], filters
ms.assetid: 019c10ab-68f6-4e40-a5e8-735b2e1270db
caps.latest.revision: 26
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 23d93e00dde20ef9d97fd707dbb938907e9ef7a9
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118868"
---
# <a name="filter-a-trace"></a>Filtrar um rastreamento
  Os filtros limitam os eventos coletados em um rastreamento. Se não houver um filtro definido, serão retornados todos os eventos das classes de evento selecionadas na saída do rastreamento. Por exemplo, limitar os nomes de usuário do Windows em um rastreamento a usuários específicos restringe os dados de saída apenas a esses usuários.  
  
 Não é obrigatório definir um filtro para um rastreamento. Porém, um filtro minimiza a sobrecarga incorrida durante um rastreamento. O filtro retorna dados focados e, logo, facilita a análise e a auditoria do desempenho.  
  
 Para filtrar os dados de eventos capturados em um rastreamento, selecione critérios de evento que retornem apenas dados relevantes do rastreamento. Por exemplo, você pode incluir ou excluir do rastreamento o monitoramento da atividade de um aplicativo específico.  
  
> [!NOTE]  
>  Quando o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] cria rastreamentos, ele exclui, por padrão, a sua própria atividade.  
  
 Um outro exemplo: se você monitorar consultas para determinar os lotes de execução mais demorada, defina critérios de evento de rastreamento de modo a monitorar apenas os lotes cuja execução leve mais de 30 segundos (valor mínimo de CPU de 30.000 milissegundos).  
  
## <a name="filter-creation-guidelines"></a>Diretrizes para a criação de filtros  
 Em geral, siga estas etapas para filtrar um rastreamento.  
  
1.  Identifique os eventos que deseja incluir no rastreamento.  
  
2.  Identifique os dados e colunas de dados que contêm as informações de que necessita.  
  
3.  Identifique o subconjunto dos dados de que necessita e defina filtros de acordo com ele.  
  
 Por exemplo, talvez lhe interesse apenas eventos que tenham certa duração ou mais. Você pode criar um rastreamento que inclua eventos em que a coluna de dados **Duration** é maior que 300 milissegundos. Seu rastreamento não incluirá eventos que terminem em menos de 300 milissegundos.  
  
 Você pode criar filtros por meio do SQL Server Profiler ou de procedimentos armazenados de Transact-SQL.  
  
 **Para filtrar eventos em um modelo de rastreamento**  
  
 [Filtrar eventos em um rastreamento &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/filter-events-in-a-trace-sql-server-profiler.md)  
  
 [Definir um filtro de rastreamento &#40;Transact-SQL&#41;](../../ssms/agent/set-sql-server-alias-for-sql-server-agent-service-ssms.md)  
  
 **Para modificar filtros**  
  
 [Modificar um filtro &#40;SQL Server Profiler&#41;](../../tools/sql-server-profiler/modify-a-filter-sql-server-profiler.md)  
  
 A disponibilidade do filtro depende da coluna de dados. Algumas colunas de dados não podem ser filtradas. As colunas de dados que podem ser filtradas só o podem por certos operadores relacionais, como mostra a tabela a seguir.  
  
|Operador relacional|Símbolo do operador|Description|  
|-------------------------|---------------------|-----------------|  
|Como|Como|Especifica que os dados de evento de rastreamento devem ser semelhantes ao texto digitado. Permite vários valores.|  
|Não semelhante a|Não semelhante a|Especifica que os dados de evento de rastreamento não devem ser semelhantes ao texto digitado. Permite vários valores.|  
|Igual a|=|Especifica que os dados de evento de rastreamento devem ser iguais ao valor digitado. Permite vários valores.|  
|É diferente de|<>|Especifica que os dados de evento de rastreamento devem ser diferentes do valor digitado. Permite vários valores.|  
|Maior que|>|Especifica que os dados de evento de rastreamento devem ser maiores que o valor digitado.|  
|Maior que ou igual a|>=|Especifica que os dados de evento de rastreamento devem ser iguais ou maiores que o valor digitado.|  
|Menor que|<|Especifica que os dados de evento de rastreamento devem ser menores que o valor digitado.|  
|Menor que ou igual a|<=|Especifica que os dados de evento de rastreamento devem ser iguais ou menores que o valor digitado.|  
  
 A tabela a seguir lista as colunas de dados que podem ser filtradas e os operadores relacionais disponíveis.  
  
|Colunas de dados|Operadores relacionais|  
|------------------|--------------------------|  
|**ApplicationName**|LIKE, NOT LIKE|  
|**BigintData1**|=, <>, >=, <=|  
|**BigintData2**|=, <>, >=, <=|  
|**BinaryData**|Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar eventos nesta coluna de dados. Para obter mais informações, consulte [Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**ClientProcessID**|=, <>, >=, <=|  
|**ColumnPermissions**|=, <>, >=, <=|  
|**CPU**|=, <>, >=, <=|  
|**DatabaseID**|=, <>, >=, <=|  
|**DatabaseName**|LIKE, NOT LIKE|  
|**DBUserName**|LIKE, NOT LIKE|  
|**Duration**|=, <>, >=, \<=|  
|**EndTime**|>=, <=|  
|**Erro**|=, <>, >=, <=|  
|**EventSubClass**|=, <>, >=, <=|  
|**FileName**|LIKE, NOT LIKE|  
|**GUID**|Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar eventos nesta coluna de dados. Para obter mais informações, consulte [Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**Handle**|=, <>, >=, <=|  
|**HostName**|LIKE, NOT LIKE|  
|**IndexID**|=, <>, >=, <=|  
|**IntegerData**|=, <>, >=, <=|  
|**IntegerData2**|=, <>, >=, <=|  
|**IsSystem**|=, <>, >=, <=|  
|**LineNumber**|=, <>, >=, <=|  
|**LinkedServerName**|LIKE, NOT LIKE|  
|**LoginName**|LIKE, NOT LIKE|  
|**LoginSid**|Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar eventos nesta coluna de dados. Para obter mais informações, consulte [Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**MethodName**|LIKE, NOT LIKE|  
|**Modo**|=, <>, >=, <=|  
|**NestLevel**|=, <>, >=, <=|  
|**NTDomainName**|LIKE, NOT LIKE|  
|**NTUserName**|LIKE, NOT LIKE|  
|**ObjectID**|=, <>, >=, <=|  
|**ObjectID2**|=, <>, >=, <=|  
|**ObjectName**|LIKE, NOT LIKE|  
|**ObjectType**|=, <>, >=, <=|  
|**Deslocamento**|=, <>, >=, <=|  
|**OwnerID**|=, <>, >=, <=|  
|**OwnerName**|LIKE, NOT LIKE|  
|**ParentName**|LIKE, NOT LIKE|  
|**Permissões**|=, <>, >=, <=|  
|**ProviderName**|LIKE, NOT LIKE|  
|**Reads**|=, <>, >=, <=|  
|**RequestID**|=, <>, >=, <=|  
|**RoleName**|LIKE, NOT LIKE|  
|**RowCounts**|=, <>, >=, <=|  
|**SessionLoginName**|LIKE, NOT LIKE|  
|**Severity**|=, <>, >=, <=|  
|**SourceDatabaseID**|=, <>, >=, <=|  
|**SPID**|=, <>, >=, \<=|  
|**SqlHandle**|Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar eventos nesta coluna de dados. Para obter mais informações, consulte [Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**StartTime**|>=, <=|  
|**Estado**|=, <>, >=, <=|  
|**Êxito**|=, <>, >=, <=|  
|**TargetLoginName**|LIKE, NOT LIKE|  
|**TargetLoginSid**|Use o [!INCLUDE[ssSqlProfiler](../../includes/sssqlprofiler-md.md)] para filtrar eventos nesta coluna de dados. Para obter mais informações, consulte [Filtrar rastreamentos com o SQL Server Profiler](../../tools/sql-server-profiler/filter-traces-with-sql-server-profiler.md).|  
|**TargetUserName**|LIKE, NOT LIKE|  
|**TextData** <sup>1</sup>|LIKE, NOT LIKE|  
|**TransactionID**|=, <>, >=, <=|  
|**Tipo**|=, <>, >=, <=|  
|**Writes**|=, <>, >=, <=|  
|**XactSequence**|=, <>, >=, <=|  
  
 <sup>1</sup> se rastrear eventos do **osql** utilitário ou **sqlcmd** utilitário, sempre acrescente **%** aos filtros na **TextData**  coluna de dados.  
  
 Por precaução em razão da segurança, o Rastreamento do SQL omite do rastreamento, automaticamente, toda informação dos procedimentos armazenados relacionados que afetem senhas. Este mecanismo de segurança não é configurável e está sempre em vigor. Ele impede os usuários que detêm permissões para rastrear toda a atividade no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]de capturar senhas.  
  
 Os seguintes procedimentos armazenados relacionados à segurança são monitorados, mas nenhuma saída é gravada na coluna de dados **TextData** :  
  
 [sp_addapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addapprole-transact-sql)  
  
 [sp_adddistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistpublisher-transact-sql)  
  
 [sp_adddistributiondb &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributiondb-transact-sql)  
  
 [sp_adddistributor &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-adddistributor-transact-sql)  
  
 [sp_addlinkedserver &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedserver-transact-sql)  
  
 [sp_addlinkedsrvlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlinkedsrvlogin-transact-sql)  
  
 [sp_addlogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addlogin-transact-sql)  
  
 [sp_addmergepullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addmergepullsubscription-agent-transact-sql)  
  
 [sp_addpullsubscription_agent &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addpullsubscription-agent-transact-sql)  
  
 [sp_addremotelogin &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addremotelogin-transact-sql)  
  
 [sp_addsubscriber &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-addsubscriber-transact-sql)  
  
 [sp_approlepassword &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-approlepassword-transact-sql)  
  
 [sp_changedistpublisher &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changedistpublisher-transact-sql)  
  
 [sp_changesubscriber &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-changesubscriber-transact-sql)  
  
 [sp_dsninfo &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-dsninfo-transact-sql)  
  
 [sp_helpsubscription_properties &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-helpsubscription-properties-transact-sql)  
  
 [sp_link_publication &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-link-publication-transact-sql)  
  
 [sp_password &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-password-transact-sql)  
  
 [sp_setapprole &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/sp-setapprole-transact-sql)  
  
  
