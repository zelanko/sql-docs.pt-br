---
title: Monitorando consultas ativas (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: craigg
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: ''
ms.component: ''
ms.technology: mpp-data-warehouse
ms.custom: ''
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: bb73f790-0537-414b-8dc2-f1eb69b92362
caps.latest.revision: 7
ms.openlocfilehash: 8a792e8dc4f29a257568f37350ba1b2c792c88fe
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="monitoring-active-queries"></a>Monitorando consultas ativas
Este tópico mostra como usar o Console de administração e as exibições do sistema SQL Server PDW para monitorar consultas ativas. Consulte [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md) e [exibições do sistema](tsql-system-views.md) para obter informações sobre essas ferramentas.  
  
## <a name="prerequisites"></a>Prerequisites  
Independentemente do método usado para monitorar consultas ativas, o logon deve ter as permissões descritas em "Usar todos os do Console de administração" [conceder permissões para usar o Console de administração](grant-permissions.md#grant-permissions-to-use-the-admin-console).  
  
## <a name="PermsAdminConsole"></a>Consultas ativas do monitor  
O Console de administração e as exibições do sistema SQL Server PDW podem ser usadas para monitorar consultas ativas. Siga as instruções abaixo.  
  
### <a name="to-monitor-active-queries-by-using-the-admin-console"></a>Para monitorar consultas ativas usando o Console de administração  
  
1.  Faça logon no Console do administrador. Consulte [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md) para obter instruções.  
  
2.  No menu superior, clique em **consultas**. Você verá uma tabela com informações básicas sobre as consultas mais recentes no dispositivo, incluindo o logon que enviou a consulta, os horários de início e término para a consulta e o status atual da consulta.  
  
3.  Para ver o comando de consulta, passe o ponteiro do mouse sobre a ID de consulta na coluna à esquerda para aquela linha.  
  
    Clique em Ajuda para ver que informações mais detalhadas sobre uma determinada consulta, a ID da consulta. Você verá informações, incluindo a consulta completa e o plano de consulta, com informações de status para cada etapa na execução da consulta. Se os erros foram retornados, você também pode ver informações detalhadas sobre os erros. <!-- MISSING LINKS See [Understanding Query Plans &#40;SQL Server PDW&#41;](../sqlpdw/understanding-query-plans-sql-server-pdw.md) for information on how to interpret the query plan information available in the Admin Console.  -->
  
### <a name="to-monitor-active-queries-by-using-the-system-views"></a>Para monitorar consultas ativas usando as exibições do sistema  
É o modo de exibição do sistema principal usado para monitorar consultas [sys.dm_pdw_exec_requests](../relational-databases/system-dynamic-management-views/sys-dm-pdw-exec-requests-transact-sql.md). Use este modo de exibição do sistema para localizar o `request_id` para uma consulta ativa ou recente, com base no texto da consulta.  
  
Por exemplo, a consulta a seguir localiza o `request_id` e atual `status` para qualquer consulta que seleciona todas as colunas da `memberAddresses` tabela.  
  
```sql  
SELECT request_id, command, status   
FROM sys.dm_pdw_exec_requests   
WHERE command   
LIKE ‘%SELECT * FROM db1..memberAddresses%’;  
```  
  
Após o `request_id` foi identificado para uma consulta, use as outras informações no `dm_pdw_exec_requests` para saber mais sobre o processamento da consulta de tabela, ou use [sys.dm_pdw_request_steps](../relational-databases/system-dynamic-management-views/sys-dm-pdw-request-steps-transact-sql.md) para exibir o status de uma consulta individual etapas para a execução da consulta.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
