---
title: sys. dm_exec_cursors (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/09/2016
ms.prod: sql
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sys.dm_exec_cursors_TSQL
- dm_exec_cursors
- dm_exec_cursors_TSQL
- sys.dm_exec_cursors
dev_langs:
- TSQL
helpviewer_keywords:
- sys.dm_exec_cursors dynamic management function
ms.assetid: f520b63c-36af-40f1-bf71-6901d6331d3d
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f2482e9af7451463c03bb5deb2e63c7261ec5361
ms.sourcegitcommit: f7ac1976d4bfa224332edd9ef2f4377a4d55a2c9
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2020
ms.locfileid: "85882042"
---
# <a name="sysdm_exec_cursors-transact-sql"></a>sys.dm_exec_cursors (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna informações sobre os cursores que estão abertos em vários bancos de dados.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
dm_exec_cursors (session_id | 0 )  
```  
  
## <a name="arguments"></a>Argumentos  
 *session_id* | 0  
 ID da sessão. Se *session_id* for especificado, essa função retornará informações sobre cursores na sessão especificada.  
  
 Se 0 for especificado, esta função retornará informações sobre todos os cursores em todas as sessões.  
  
## <a name="table-returned"></a>Tabela retornada  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**session_id**|**int**|ID da sessão que detém o cursor.|  
|**cursor_id**|**int**|ID do objeto do cursor.|  
|**name**|**nvarchar(256)**|Nome do cursor como definido pelo usuário.|  
|**properties**|**nvarchar(256)**|Especifica as propriedades do cursor. Os valores das seguintes propriedades são concatenados para formar o valor desta coluna:<br />Interface de declaração<br />Tipo de cursor <br />Simultaneidade de cursores<br />Escopo do cursor<br />Nível de aninhamento do cursor<br /><br /> Por exemplo, o valor retornado nesta coluna pode ser "TSQL &#124; dinâmico &#124; otimista &#124; global (0)".|  
|**sql_handle**|**varbinary(64)**|Identificador do texto do lote que declarou o cursor.|  
|**statement_start_offset**|**int**|Número de caracteres no procedimento em lote ou armazenado atualmente em execução no qual a instrução atualmente em execução se inicia. Pode ser usado junto com o **sql_handle**, o **statement_end_offset**e a função de gerenciamento dinâmico [Sys. dm_exec_sql_text](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md) para recuperar a instrução atualmente em execução para a solicitação.|  
|**statement_end_offset**|**int**|Número de caracteres no procedimento em lote ou armazenado atualmente em execução no qual a instrução atualmente em execução termina. Pode ser usado junto com o **sql_handle**, o **statement_start_offset**e a função de gerenciamento dinâmico **Sys. dm_exec_sql_text** para recuperar a instrução atualmente em execução para a solicitação.|  
|**plan_generation_num**|**bigint**|Um número de sequência que pode ser usado para distinguir entre instâncias de planos após uma recompilação.|  
|**creation_time**|**datetime**|Carimbo de data e hora da criação do cursor.|  
|**is_open**|**bit**|Especifica se o cursor está aberto.|  
|**is_async_population**|**bit**|Especifica se o thread em segundo plano ainda está populando assincronamente um cursor KEYSET ou STATIC.|  
|**is_close_on_commit**|**bit**|Especifica se o cursor foi declarado por meio de CURSOR_CLOSE_ON_COMMIT.<br /><br /> 1 = O cursor será fechado quando a transação terminar.|  
|**fetch_status**|**int**|Retorna o último status de busca do cursor. Este é o último valor de @ retornado @FETCH_STATUS .|  
|**fetch_buffer_size**|**int**|Retorna informações sobre o tamanho do buffer de busca.<br /><br /> 1 = Cursores Transact-SQL. Pode ser definido como um valor mais alto para cursores de API.|  
|**fetch_buffer_start**|**int**|No caso dos cursores FAST_FORWARD e DYNAMIC, retornará 0 se o cursor não estiver aberto ou se for posicionado antes da primeira linha. Caso contrário, ele retornará -1.<br /><br /> No caso dos cursores STATIC e KEYSET, retornará 0, se o cursor não estiver aberto, e -1, se o cursor for posicionado antes da primeira linha.<br /><br /> Caso contrário, retorna o número da linha onde está posicionado.|  
|**ansi_position**|**int**|Posição de cursor dentro do buffer de busca.|  
|**worker_time**|**bigint**|Tempo gasto, em microssegundos, pelos trabalhados que executam este cursor.|  
|**reads**|**bigint**|Número de leituras executadas pelo cursor.|  
|**writes**|**bigint**|Número de gravações executadas pelo cursor.|  
|**dormant_duration**|**bigint**|Milissegundos desde o início da última consulta (aberta ou de busca) neste cursor.|  
  
## <a name="permissions"></a>Permissões  
 , é necessário ter permissão VIEW SERVER STATE no servidor.  
  
## <a name="remarks"></a>Comentários  
 A tabela a seguir fornece informações sobre a interface de declaração de cursor e inclui os valores possíveis para a coluna de propriedades.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|API|O cursor foi declarado usando uma das APIs de acesso a dados (ODBC, OLEDB).|  
|TSQL|O cursor foi declarado usando a sintaxe DECLARE CURSOR de Transact-SQL.|  
  
 A tabela a seguir fornece informações sobre o tipo de cursor e inclui os valores possíveis para a coluna de propriedades.  
  
|Type|Description|  
|----------|-----------------|  
|Keyset|O cursor foi declarado como Keyset (conjunto de chaves).|  
|Dinâmico|O cursor foi declarado como Dynamic (dinâmico).|  
|Instantâneo|O cursor foi declarado como Snapshot (instantâneo) ou Static (estático).|  
|Fast_Forward|O cursor foi declarado como Fast Forward (avanço rápido).|  
  
 A tabela a seguir fornece informações sobre o tipo de simultaneidade de cursores e inclui os valores possíveis para a coluna de propriedades.  
  
|Simultaneidade|Descrição|  
|-----------------|-----------------|  
|Somente leitura|O cursor foi declarado como somente leitura.|  
|Scroll Locks|O cursor usa bloqueios de rolagem.|  
|Otimistas|O cursor usa controle de simultaneidade otimista.|  
  
 A tabela a seguir fornece informações sobre o tipo de escopo de cursor e inclui os valores possíveis para a coluna de propriedades.  
  
|Escopo|Descrição|  
|-----------|-----------------|  
|Local|Especifica que o escopo do cursor é local para o lote, procedimento armazenado ou gatilho no qual o cursor foi criado.|  
|Global|Especifica que o escopo do cursor é global para a conexão.|  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-detecting-old-cursors"></a>a. Detectando cursores antigos  
 Este exemplo retorna informações sobre cursores que estiveram abertos no servidor por mais tempo que as 36 horas especificadas.  
  
```  
SELECT creation_time, cursor_id, name, c.session_id, login_name   
FROM sys.dm_exec_cursors(0) AS c   
JOIN sys.dm_exec_sessions AS s ON c.session_id = s.session_id   
WHERE DATEDIFF(hh, c.creation_time, GETDATE()) > 36;  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Funções e exibições de gerenciamento dinâmico &#40;Transact-SQL&#41;](~/relational-databases/system-dynamic-management-views/system-dynamic-management-views.md)   
 [Funções e exibições de gerenciamento dinâmico relacionadas à execução &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/execution-related-dynamic-management-views-and-functions-transact-sql.md)   
 [sys.dm_exec_sessions &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sessions-transact-sql.md)  
  
  

