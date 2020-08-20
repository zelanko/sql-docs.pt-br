---
description: MSSQLSERVER_2814
title: MSSQLSERVER_2814 | Microsoft Docs
ms.custom: ''
ms.date: 07/11/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: supportability
ms.topic: language-reference
helpviewer_keywords:
- 2814 (Database Engine error)
ms.assetid: 22800748-9be9-4511-9428-6b8b40e5bef9
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 174836221e6040bde4fff244e3d5377f90b0089e
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482715"
---
# <a name="mssqlserver_2814"></a>MSSQLSERVER_2814
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  
## <a name="details"></a>Detalhes  
  
| Atributo | Valor |  
| :-------- | :---- |  
|Nome do Produto|SQL Server|  
|ID do evento|2814|  
|Origem do Evento|MSSQLSERVER|  
|Componente|SQLEngine|  
|Nome simbólico|PR_POSSIBLE_INFINITE_RECOMPILE|  
|Texto da mensagem|Uma possível recompilação infinita foi detectada para SQLHANDLE %hs, PlanHandle %hs, deslocamento inicial %d, deslocamento final %d. O último motivo da recompilação foi %d.|  
  
## <a name="explanation"></a>Explicação  
Uma ou mais instruções fizeram com que o lote de consultas fosse recompilado pelo menos 50 vezes. A instrução especificada deve ser corrigida para evitar mais recompilações.  
  
A tabela a seguir lista os motivos da recompilação.  
  
|Código do motivo|Descrição|  
|---------------|---------------|  
|1|Esquema alterado|  
|2|Estatísticas alteradas|  
|3|Compilação adiada|  
|4|Opção set alterada|  
|5|Tabela temp alterada|  
|6|Conjunto de linhas remoto alterado|  
|7|Permissões For Browse alteradas|  
|8|Ambiente de notificação de consulta alterado|  
|9|Exibição de partição alterada|  
|10|Opções de cursor alteradas|  
|11|Opção (recompilar) solicitada|  
  
## <a name="user-action"></a>Ação do usuário  
  
1.  Para exibir a instrução que causa a recompilação, execute a consulta a seguir. Substitua os espaços reservados *sql_handle*, *starting_offset*, *ending_offset* e *plan_handle* pelos valores especificados na mensagem de erro. As colunas **database_name** e **object_name** são NULL para instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] ad hoc e preparadas.  
  
    ```sql   
    SELECT DB_NAME(st.dbid) AS database_name,  
        OBJECT_NAME(st.objectid) AS object_name,  
        st.text  
    FROM sys.dm_exec_query_stats AS qs  
    CROSS APPLY sys.dm_exec_sql_text (*sql_handle*) AS st  
    WHERE qs.statement_start_offset = *starting_offset*  
    AND qs.statement_end_offset = *ending_offset*  
    AND qs.plan_handle = *plan_handle*;
    ```
  
2.  Com base na descrição do código do motivo, modifique a instrução, o lote ou o procedimento para evitar recompilações. Por exemplo, um procedimento armazenado pode conter uma ou mais instruções SET. Essas instruções devem ser removidas do procedimento. Para obter mais exemplos dos motivos e das resoluções da recompilação, consulte [Problemas de compilação em lote, recompilação e cache de planos no SQL Server 2005](/previous-versions/sql/sql-server-2005/administrator/cc966425(v=technet.10)).  
  
3.  Se o problema persistir, contate os Serviços de Atendimento ao Cliente da Microsoft.  
  
## <a name="see-also"></a>Consulte Também  
[Classe de evento SQL:StmtRecompile](../event-classes/sql-stmtrecompile-event-class.md)  
  
