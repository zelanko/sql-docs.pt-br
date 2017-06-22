---
title: "SQL Server, objeto Métodos de Acesso | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Access Methods object
- SQLServer:Access Methods
ms.assetid: 27558585-e780-48bb-a042-30d664662ebc
caps.latest.revision: 36
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 19dcb59cbc63c0c956604fb5745f8446da067642
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="sql-server-access-methods-object"></a>SQL Server, Objeto Métodos de Acesso
  O objeto **Access Methods** no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece contadores para monitorar como são acessados os dados lógicos dentro do banco de dados. O acesso físico às páginas do banco de dados no disco é monitorado usando os contadores do **Gerenciador de Buffer** . Monitorar os métodos usados para acessar os dados armazenados no banco de dados pode ajudá-lo a determinar se o desempenho da consulta pode ser melhorado, adicionando ou modificando índices, adicionando ou movendo partições, adicionando arquivos ou grupos de arquivo, desfragmentando índices ou regravando consultas. Os contadores dos **Métodos de Acesso** também podem ser usados para monitorar a quantidade de dados, índices e espaço livre dentro do banco de dados, indicando assim o volume e a fragmentação de dados para cada instância do servidor. A fragmentação excessiva do índice pode prejudicar o desempenho.  
  
 Para obter informações mais detalhadas sobre volume, fragmentação e uso de dados, use as seguintes exibições de gerenciamento dinâmico:  
  
-   [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md)  
  
-   [sys.dm_db_index_physical_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-physical-stats-transact-sql.md)  
  
-   [sys.dm_db_partition_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-partition-stats-transact-sql.md)  
  
-   [sys.dm_db_index_usage_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-usage-stats-transact-sql.md)  
  
 Para consumo de espaço em **tempdb** no arquivo, tarefa e nível de sessão, use essas exibições de gerenciamento dinâmico:  
  
-   [sys.dm_db_file_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-file-space-usage-transact-sql.md)  
  
-   [sys.dm_db_task_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-task-space-usage-transact-sql.md)  
  
-   [sys.dm_db_session_space_usage &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-session-space-usage-transact-sql.md)  
  
 Esta tabela descreve os contadores dos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **Access Methods** .  
  
|Contadores dos Métodos de Acesso do SQL Server|Descrição|  
|----------------------------------------|-----------------|  
|**Lotes de limpeza de unidade de alocação/s**|O número de lotes por segundo concluídos com êxito pela tarefa em segundo plano responsável pela limpeza de unidades de alocação canceladas e adiadas.|  
|**Limpezas de unidade de alocação/s**|O número de unidades de alocação por segundo descartadas com sucesso pela tarefa em segundo plano responsável pela limpeza das unidades de alocação canceladas e adiadas. Cada descarte de unidade de alocação requer vários lotes.|  
|**Contagem de Criação de LOB por Referência**|Contagem de valores de LOB (objeto grande) que foram transmitidos por referência. LOBs por referência são usados em determinadas operações em massa para evitar o custo de transmiti-los por valor.|  
|**Contagem de Uso de LOB por referência**|Contagem de valores de LOB por referência que foram usados. LOBs por referência são usados em determinadas operações em massa para evitar o custo de transmiti-los por valor.|  
|**Contagem de LOBs lidos antecipadamente**|Contagem de páginas de LOB com emissão de leitura antecipada.|  
|**Contar pull em linha**|Contagem de valores da coluna que foram puxadas para dentro da linha.|  
|**Contar Push para fora da linha**|Contagem de valores da coluna que foram empurrados para fora da linha.|  
|**Unidades de alocação adiadas ignoradas**|O número de unidades de alocação aguardando para serem descartadas pela tarefa em segundo plano responsável pela limpeza das unidades de alocação canceladas e adiadas.|  
|**Conjunto de Linhas Adiado Ignorado**|O número de conjuntos de linhas criados como resultado de operações anuladas de compilação de índices online, que estão aguardando para serem descartados pela tarefa em segundo plano responsável pela limpeza dos conjuntos de linhas adiado ignorado.|  
|**Limpezas no conjunto de linhas ignorado/s**|O número de conjuntos de linhas, por segundo criados como resultado de operações anuladas de compilação de índices online, que foram cancelados com êxito pela tarefa em segundo plano responsável pela limpeza de conjuntos de linhas cancelados e adiados.|  
|**Conjuntos de linhas ignorados/s**|O número de conjuntos de linhas por segundo, criados como resultado de operações anuladas de compilação de índices online, que foram ignorados pela tarefa em segundo plano responsável pela limpeza de conjuntos de linhas cancelados e adiados criados.|  
|**Desalocações de Extensão/s**|Número de extensões desalocadas por segundo em todos os bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Extensões Alocadas/s**|Número de extensões alocadas por segundo em todos os bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].|  
|**Falha em lotes de limpeza de unidade de alocação/s**|O número de lotes por segundo que apresentaram falhas e precisaram ser repetidos pela tarefa em segundo plano responsável pela limpeza das unidades de alocação canceladas e adiadas. As falhas podem estar relacionadas à falta de memória ou de espaço no disco, a uma falha de hardware ou outros motivos.|  
|**Falha no cookie na página de folha**|O número de vezes em que não foi possível usar um cookie na página de folha durante uma pesquisa de índice, devido a alterações que ocorreram nessa página de folha. O cookie é usado para acelerar a pesquisa de índice.|  
|**Falha no cookie na página de árvore**|O número de vezes em que não foi possível usar um cookie na página de árvore durante uma pesquisa de índice, devido a alterações que ocorreram nas páginas pai dessas páginas de árvore. O cookie é usado para acelerar a pesquisa de índice.|  
|**Registros Encaminhados/s**|Número de registros por segundo encontrados por ponteiros de registros encaminhados.|  
|**Buscas de Página de Espaço Livre/s**|Número de páginas encontradas por segundo por exames de espaço livre. Esses exames pesquisam o espaço livre em páginas já alocadas a uma unidade de alocação para atender a solicitações ou para inserir ou modificar fragmentos de registro.|  
|**Exames de Espaço Livre/s**|Número de exames por segundo que foram iniciados para pesquisar espaço livre em páginas já alocadas a uma unidade de alocação para inserir ou modificar fragmento de registro. Cada exame pode localizar várias páginas.|  
|**Exames Totais/s**|Número de exames totais irrestritos por segundo. Eles podem ser exames da tabela base ou do índice total.|  
|**Pesquisas de Índice/s**|Número de pesquisas de índice por segundo. Eles são usados para iniciar exames de intervalo, reposicionar um exame de intervalo, revalidar um ponto de exame, buscar um registro de índice único e procurar o índice para localizar onde inserir uma nova linha.|  
|**Esperas de InSysXact/s**|Número de vezes que um leitor precisa aguardar uma página porque o bit InSysXact está definido.|  
|**Contagem de Criação de LobHandle**|Contagem de LOBs temporários criados.|  
|**Contagem de Destruição de LobHandle**|Contagem de LOBs temporários destruídos.|  
|**Contagem de Criação de Provedor LobSS**|Contagem de SSPs (Provedores de Serviço de Armazenamento) de LOB criados. Uma tabela de trabalho criada por SSP de LOB.|  
|**Contagem de Destruição de Provedor LobSS**|Contagem de SSP de LOB destruído.|  
|**Contagem de Truncamento de Provedor LobSS**|Contagem de SSP de LOB truncado.|  
|**Alocações de página mistas/s**|Número de páginas alocadas por segundo a partir de extensões mistas. Essas páginas podem ser usadas para armazenar as páginas IAM e as primeiras oito páginas alocadas a uma unidade de alocação.|  
|**Tentativas de compactação de página/s**|Número de páginas avaliadas para a compactação do nível de página. Inclui as páginas que não foram compactadas porque poderia haver economias significativas. Inclui todos os objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre objetos específicos, veja [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Desalocações de Página/s**|Número de páginas desalocadas por segundo em todos os bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Páginas de extensões mistas e de extensões uniformes estão incluídas.|  
|**Divisões de Página/s**|Número de divisões de página por segundo que ocorrem em decorrência do estouro de páginas de índice.|  
|**Páginas Alocadas/s**|Número de páginas alocadas por segundo em todos os bancos de dados nesta instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Elas incluem alocações de páginas a partir de extensões mistas e de extensões uniformes.|  
|**Páginas compactadas/s**|Número de páginas de dados compactadas usando compactação de PÁGINA. Inclui todos os objetos na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter informações sobre objetos específicos, veja [sys.dm_db_index_operational_stats &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-db-index-operational-stats-transact-sql.md).|  
|**Exames de Sondagem/s**|Número de exames de sondagem por segundo usados para localizar no máximo uma linha qualificada em um índice ou em uma tabela base diretamente.|  
|**Exames de Intervalo/s**|Número de exames de intervalo qualificados em índices por segundo.|  
|**Revalidações de Ponto de Exame/s**|Número de vezes por segundo que o ponto de exame teve que ser revalidado para continuar o exame.|  
|**Registros Fantasmas Ignorados/s**|Número de registros fantasmas por segundo ignorados durante exames.|  
|**Escalações de Bloqueio de Tabela/s**|Número de vezes que bloqueios em uma tabela foram escalados para a granularidade TABELA ou HoBT.|  
|**Cookie usado na página de folha**|Número de vezes que um cookie na página de folha foi usado com êxito durante uma pesquisa de índice, pois nenhuma alteração ocorreu nesta página de folha. O cookie é usado para acelerar a pesquisa de índice.|  
|**Cookie usado na página de árvore**|Número de vezes que um cookie na página de árvore foi usado com êxito durante uma pesquisa de índice, pois nenhuma alteração ocorreu na página pai dessa página de árvore. O cookie é usado para acelerar a pesquisa de índice.|  
|**Arquivos de Trabalho Criados/s**|Número de arquivos de trabalho criados por segundo. Por exemplo, os arquivos de trabalho podem ser usados para armazenar os resultados temporários de junções de hash e de agregações de hash.|  
|**Tabelas de Trabalho Criadas/s**|Número de tabelas de trabalho criadas por segundo. Por exemplo, tabelas de trabalho podem ser usadas para armazenar os resultados temporários de spool de consultas, variáveis LOB, variáveis XML e cursores.|  
|**Tabelas de Trabalho do Cache Base**|Somente para uso interno.|  
|**Taxas de Tabela de Trabalho do Cache**|Porcentagem de tabelas de trabalho criadas em que as duas páginas iniciais de uma determinada tabela não estavam alocadas, mas estavam imediatamente disponíveis no cache de tabelas de trabalho. (Quando uma tabela de trabalho é descartada, duas páginas podem permanecer alocadas e são retornadas ao cache de tabelas de trabalho. Isto aumenta o desempenho.)|  
  
## <a name="see-also"></a>Consulte também  
 [Monitorar o uso de recursos &#40;Monitor do Sistema&#41;](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)  
  
  
