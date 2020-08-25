---
title: Monitorar consultas ativas
description: Use o console de administração e as exibições paralelas do sistema de data warehouse para monitorar consultas ativas no sistema de plataforma de análise.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 9157db745b999711966f0019747ba1d61823569e
ms.sourcegitcommit: 33e774fbf48a432485c601541840905c21f613a0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/25/2020
ms.locfileid: "74400912"
---
# <a name="monitoring-active-queries---parallel-data-warehouse"></a>Monitorando consultas ativas – data warehouse paralelos
Este artigo mostra como usar o console de administração do e o SQL Server PDW exibições do sistema para monitorar consultas ativas. Consulte [monitorar o dispositivo usando o console de administração](monitor-the-appliance-by-using-the-admin-console.md) e [exibições do sistema](tsql-system-views.md) para obter informações sobre essas ferramentas.  
  
## <a name="prerequisites"></a>Pré-requisitos  
Independentemente do método usado para monitorar consultas ativas, o logon deve ter as permissões descritas em "usar todo o console de administração" em [conceder permissões para usar o console de administração](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="monitor-active-queries"></a><a name="PermsAdminConsole"></a>Monitorar consultas ativas  
Tanto o console de administração do quanto o SQL Server PDW exibições do sistema podem ser usados para monitorar consultas ativas. Siga as instruções abaixo.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Para monitorar consultas ativas usando o console de administração  
  
1.  Faça logon no console de administração. Consulte [monitorar o dispositivo usando o console de administração](monitor-the-appliance-by-using-the-admin-console.md) para obter instruções.  
  
2.  No menu superior, clique em **consultas**. Você verá uma tabela com informações básicas sobre as consultas mais recentes no dispositivo, incluindo o logon que enviou a consulta, as horas de início e de término da consulta e o status atual da consulta.  
  
3.  Para ver o comando de consulta, passe o ponteiro do mouse sobre a ID da consulta na coluna esquerda dessa linha.  
  
    Para ver informações mais detalhadas de uma consulta específica, clique na ID da consulta. Você verá informações incluindo a consulta completa e o plano de consulta, com informações de status para cada etapa na execução da consulta. Se algum erro for retornado, você também poderá ver informações detalhadas sobre os erros. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Para monitorar consultas ativas usando as exibições do sistema  
A exibição do sistema principal usada para monitorar consultas é [Sys. dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Use esta exibição do sistema para localizar o `request_id` para uma consulta ativa ou recente, com base no texto da consulta.  
  
Por exemplo, a consulta a seguir localiza o `request_id` e o atual `status` para qualquer consulta que seleciona todas as colunas da `memberAddresses` tabela.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE '%SELECT * FROM db1..memberAddresses%';  
```  
  
Depois que o `request_id` tiver sido identificado para uma consulta, use as outras informações na `dm_pdw_exec_requests` tabela para descobrir sobre o processamento da consulta ou use [Sys. dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) para exibir o status das etapas de consulta individuais para a execução da consulta.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
