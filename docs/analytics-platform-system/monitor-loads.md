---
title: Monitorar cargas
description: Monitore as cargas ativas e recentes usando o console de administração do APS (sistema de plataforma de análise) ou as exibições do sistema do PDW (Parallel data warehouse).
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: b284fdcef506924c26e452196db6e9518faa1351
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74400963"
---
# <a name="monitor-loads-into-parallel-data-warehouse"></a>Monitorar cargas em data warehouse paralelos
Monitore cargas de [dwloader](dwloader.md) ativas e recentes usando o console de administração do APS (sistema de plataforma de análise) ou as [exibições do sistema](https://azure.microsoft.com/documentation/articles/sql-data-warehouse-reference-tsql-system-views/)do PDW (Parallel Data warehouse). 
  
> [!TIP]  
> Algumas cargas são iniciadas usando instruções INSERT ou business intelligence ferramentas que usam instruções SQL para executar a carga. 

<!-- MISSING LINKS
To monitor this type of load, see [Monitoring Active Queries](monitor-active-queries.md).  
-->
  
## <a name="prerequisites"></a>Prerequisites  
Independentemente do método usado para monitorar uma carga, o logon deve ter permissão para acessar as fontes de dados subjacentes. 

<!-- MISSING LINKS
For the permissions to grant, see "Use All of the Admin Console" in [Grant Permissions to Use the Admin Console](grant-permissions-admin-console.md). 

--> 
  
## <a name="monitoring-loads"></a>Monitoramento de cargas  
As seções a seguir descrevem como monitorar cargas.  
  
### <a name="to-monitor-loads-by-using-the-admin-console"></a>Para monitorar cargas usando o console de administração  
  
1.  Faça logon no console de administração. <!-- MISSING LINKS See [Monitor the Appliance by Using the Admin Console;](monitor-admin-console.md) for instructions. --> 
  
2.  No menu superior, clique em **cargas**. Você verá uma tabela classificável mostrando todas as cargas recentes e ativas, além de informações adicionais, como se a carga foi concluída ou se ainda está ativa. Clique nos cabeçalhos de coluna para classificar as linhas.  
  
3.  Para exibir detalhes adicionais de uma carga específica, clique na **ID** de carregamento na coluna esquerda. Na exibição detalhada, você pode ver o progresso em cada etapa da carga.  
  
Consulte essas exibições do sistema para obter informações sobre os metadados sobre a carga mostrada no console de administração:  
  
-   [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md)  
  
-   [sys.pdw_loader_run_stages](https://msdn.microsoft.com/library/mt203879.aspx)  
  
-   [sys.pdw_loader_backup_runs](../relational-databases/system-catalog-views/sys-pdw-loader-backup-runs-transact-sql.md)  
  
-   [sys.pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md)  
  
### <a name="to-monitor-loads-by-using-system-views"></a>Para monitorar cargas usando exibições do sistema  
Para monitorar as cargas ativas e recentes usando SQL Server PDW exibições, siga as etapas abaixo. Para cada exibição do sistema usada, consulte a documentação dessa exibição para obter informações sobre as colunas e os valores possíveis retornados pela exibição.  
  
1.  Localize o `request_id` para a carga na exibição [Sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md) encontrando a linha de comando Loader na `command` coluna desta exibição.  
  
    Por exemplo, o comando a seguir retorna o texto do comando e o status atual `request_id`, além do.  
  
    ```sql  
    SELECT request_id, status, command FROM sys.dm_pdw_exec_requests;  
    ```  
  
2.  Use o `request_id` para recuperar informações adicionais para a carga usando as exibições [Sys. pdw_loader_run_stages](../relational-databases/system-catalog-views/sys-pdw-loader-run-stages-transact-sql.md) e [Sys. pdw_loader_backup_run_details](../relational-databases/system-catalog-views/sys-pdw-loader-backup-run-details-transact-sql.md) . Por exemplo, a consulta a seguir retorna `run_id` as informações e sobre os horários de início, término e duração da carga, além de quaisquer erros e informações sobre o número de linhas processadas:  
  
    ```sql  
    SELECT lbr.run_id,   
    er.submit_time, er.end_time, er.total_elapsed_time, er.error_id, lbr.rows_processed, lbr.rows_rejected, lbr.rows_inserted   
    FROM sys.dm_pdw_exec_requests er   
    LEFT OUTER JOIN   
    sys.pdw_loader_backup_runs lbr   
    ON (er.request_id=lbr.requst_id)   
    WHERE er.request_id='12738';  
    ```  
  
<!-- MISSING LINKS

## See Also  
[Common metadata query examples](metadata-query-examples.md)
-->  
  
