---
description: sys.fn_trace_gettable (Transact-SQL)
title: sys. fn_trace_gettable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- fn_trace_gettable
- fn_trace_gettable_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- fn_trace_gettable function
- sys.fn_trace_gettable function
ms.assetid: c2590159-6ec5-4510-81ab-e935cc4216cd
author: rothja
ms.author: jroth
ms.openlocfilehash: 85ffb20fb0ead23c8027ab9b4ba45f906fe8c097
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88464732"
---
# <a name="sysfn_trace_gettable-transact-sql"></a>sys.fn_trace_gettable (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Retorna o conteúdo de um ou mais arquivos de rastreamento em formato de tabela.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*filename*'  
 Especifica o arquivo de rastreamento inicial a ser lido. *filename* é **nvarchar (256)**, sem padrão.  
  
 *number_files*  
 Especifica o número de arquivos de substituição a serem lidos. Esse número inclui o arquivo inicial especificado em *filename*. *number_files* é um **int**.  
  
## <a name="remarks"></a>Comentários  
 Se *number_files* for especificado como **padrão**, **fn_trace_gettable** lerá todos os arquivos de substituição até atingir o final do rastreamento. **fn_trace_gettable** retorna uma tabela com todas as colunas válidas para o rastreamento especificado. Para obter mais informações, consulte [sp_trace_setevent &#40;&#41;Transact-SQL ](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 Lembre-se de que a função fn_trace_gettable não carregará arquivos de substituição (quando essa opção for especificada usando o argumento *number_files* ) em que o nome do arquivo de rastreamento original termina com um sublinhado e um valor numérico. (Isso não se aplica ao sublinhado e ao número que são anexados automaticamente quando um arquivo é transferido.) Como alternativa, você pode renomear os arquivos de rastreamento para remover os sublinhados no nome do arquivo original. Por exemplo, se o arquivo original for denominado **Trace_Oct_5. trc** e o arquivo de substituição for nomeado **Trace_Oct_5_1. trc**, você poderá renomear os arquivos para **TraceOct5. trc** e **TraceOct5_1. trc**.  
  
 Essa função pode ler um rastreamento que ainda esteja ativo na instância na qual é executado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-fn_trace_gettable-to-import-rows-from-a-trace-file"></a>a. Usando fn_trace_gettable para importar linhas de um arquivo de rastreamento  
 O exemplo a seguir chama `fn_trace_gettable` dentro da cláusula `FROM` de uma instrução `SELECT...INTO`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fn_trace_gettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. Usando fn_trace_gettable para retornar uma tabela com uma coluna IDENTITY que pode ser carregada em uma tabela do SQL Server  
 O exemplo a seguir chama a função como parte de uma instrução `SELECT...INTO` e retorna uma tabela com uma coluna `IDENTITY` que pode ser carregada na tabela `temp_trc`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>Consulte Também  
 [&#41;&#40;Transact-SQL de sp_trace_generateevent ](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [&#41;&#40;Transact-SQL de sp_trace_setfilter ](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
