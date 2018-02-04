---
title: sys.fn_get_sql (Transact-SQL) | Microsoft Docs
ms.custom: 
ms.date: 06/10/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: system-functions
ms.reviewer: 
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- fn_get_sql
- sys.fn_get_sql_TSQL
- fn_get_sql_TSQL
- sys.fn_get_sql
dev_langs:
- TSQL
helpviewer_keywords:
- fn_get_sql function
- text [SQL Server], SQL handles
- sys.fn_get_sql function
- valid SQL handles [SQL Server]
- SQL handles
ms.assetid: d5fe49b5-0813-48f2-9efb-9187716b2fd4
caps.latest.revision: 
author: BYHAM
ms.author: rickbyh
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ad0861b72965936dfb673774a339ab7769f63689
ms.sourcegitcommit: c556eaf60a49af7025db35b7aa14beb76a8158c5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/03/2018
---
# <a name="sysfngetsql-transact-sql"></a>sys.fn_get_sql (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o texto da instrução SQL do identificador SQL especificado.  
  
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Microsoft SQL Server. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use sys.dm_exec_sql_text. Para obter mais informações, consulte [dm_exec_sql_text &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-sql-text-transact-sql.md).  
  
 
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sys.fn_get_sql ( SqlHandle )  
```  
  
## <a name="arguments"></a>Argumentos  
 *SqlHandle*  
 É o valor do identificador. *SqlHandle* é **varbinary(64)** sem nenhum padrão.  
  
## <a name="tables-returned"></a>Tabelas retornadas  
  
|Nome da coluna|Tipo de dados|Description|  
|-----------------|---------------|-----------------|  
|dbid|**smallint**|ID do banco de dados. Para instruções SQL preparadas e ad hoc, a ID do banco de dados no qual as instruções foram compiladas.|  
|objectid|**Int**|ID do objeto do banco de dados. É NULL para instruções SQL ad hoc.|  
|number|**smallint**|Indica o número do grupo e se os procedimentos estão agrupados.<br /><br /> 0 = Entradas não são procedimentos.<br /><br /> NULL = Instruções SQL ad hoc.|  
|encrypted|**bit**|Indica se o objeto está criptografado.<br /><br /> 0 = não criptografado<br /><br /> 1 = Criptografado|  
|text|**text**|É o texto da instrução SQL. É NULL para objetos criptografados.|  
  
## <a name="remarks"></a>Remarks  
 Você pode obter um identificador SQL válido da coluna sql_handle do [exec_requests &#40; Transact-SQL &#41; ](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md) exibição de gerenciamento dinâmico.  
  
 Se você passar um identificador que não existe no cache, fn_get_sq**l** retorna um conjunto de resultados vazio. Se você passar um identificador inválido, o lote parará e uma mensagem de erro será retornada.  
  
 O [!INCLUDE[ssDEnoversion](../../includes/ssdenoversion-md.md)] não é possível armazenar em cache algumas [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções, como instruções de cópia em massa e instruções com literais de cadeia de caracteres que são maiores que 8 KB. Identificadores para essas instruções não podem ser recuperados usando fn_get_sql.  
  
 O **texto** coluna do conjunto de resultados é filtrada para texto que pode conter senhas. Para mais informações relacionadas à segurança de procedimentos armazenados que não são monitorados, consulte [filtrar um rastreamento](../../relational-databases/sql-trace/filter-a-trace.md).  
  
 A função fn_get_sql retorna informações semelhantes para o [DBCC INPUTBUFFER](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md) comando. Veja, a seguir, exemplos de quando a função fn_get_sql pode ser usada, porque o DBCC INPUTBUFFER não pode ser usado:  
  
-   Quando eventos têm mais de 255 caracteres.  
  
-   Quando você tem que retornar o nível mais alto de aninhamento atual de um procedimento armazenado. Por exemplo, há dois procedimentos armazenados que são nomeados sp_1 e sp_2. Se sp_1 chamar sp_2 e você obtiver o identificador da exibição de gerenciamento dinâmico sys.dm_exec_requests enquanto sp_2 estiver sendo executado, a função fn_get_sql retornará informações sobre sp_2. Além disso, a função fn_get_sql retorna o texto completo do procedimento armazenado no nível atual de aninhamento mais alto.  
  
## <a name="permissions"></a>Permissões  
 O usuário precisa da permissão VIEW SERVER STATE no servidor.  
  
## <a name="examples"></a>Exemplos  
 Administradores de banco de dados podem usar a função fn_get_sql, conforme mostrado no exemplo a seguir, para ajudar a diagnosticar processos de problemas. Depois de identificar a ID de sessão de um problema, o administrador pode recuperar o identificador SQL daquela sessão, chamar fn_get_sql com o identificador e, em seguida, usar os deslocamentos de início e de término para determinar o texto SQL da ID de sessão do problema.  
  
```  
DECLARE @Handle varbinary(64);  
SELECT @Handle = sql_handle   
FROM sys.dm_exec_requests   
WHERE session_id = 52 and request_id = 0;  
SELECT * FROM sys.fn_get_sql(@Handle);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [DBCC INPUTBUFFER &#40;Transact-SQL&#41;](../../t-sql/database-console-commands/dbcc-inputbuffer-transact-sql.md)   
 [sys.sysprocesses &#40;Transact-SQL&#41;](../../relational-databases/system-compatibility-views/sys-sysprocesses-transact-sql.md)   
 [sys.dm_exec_requests &#40;Transact-SQL&#41;](../../relational-databases/system-dynamic-management-views/sys-dm-exec-requests-transact-sql.md)  
  
  
