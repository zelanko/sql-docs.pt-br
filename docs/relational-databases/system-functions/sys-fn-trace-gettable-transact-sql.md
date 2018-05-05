---
title: fn_trace_gettable (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-functions
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 35
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 54430ef6f0ecfd665069b4e7406a04d94ce39a05
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sysfntracegettable-transact-sql"></a>sys.fn_trace_gettable (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Retorna o conteúdo de um ou mais arquivos de rastreamento em formato de tabela.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)] Em vez disso, use Eventos Estendidos.  
   
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
fn_trace_gettable ( 'filename' , number_files )  
```  
  
## <a name="arguments"></a>Argumentos  
 '*filename*'  
 Especifica o arquivo de rastreamento inicial a ser lido. *nome de arquivo* é **nvarchar (256)**, sem padrão.  
  
 *number_files*  
 Especifica o número de arquivos de substituição a serem lidos. Esse número inclui o arquivo inicial especificado em *filename*. *number_files* é um **int**.  
  
## <a name="remarks"></a>Remarks  
 Se *number_files* é especificado como **padrão**, **fn_trace_gettable** lerá todos os arquivos de substituição até atingir o final do rastreamento. **fn_trace_gettable** retorna uma tabela com todas as colunas válidas para o rastreamento especificado. Para obter mais informações, consulte [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md).  
  
 Lembre-se de que a função fn_trace_gettable não carregará arquivos de substituição (quando esta opção é especificada usando o *number_files* argumento) onde o nome do arquivo de rastreamento original termina com um sublinhado e um valor numérico. (Isso não se aplica ao sublinhado e ao número que são acrescentados automaticamente quando um arquivo é substituído.) Como alternativa, você pode renomear os arquivos de rastreamento para remover os sublinhados no nome de arquivo original. Por exemplo, se o arquivo original é chamado **Trace_Oct_5.trc** e o arquivo de substituição nomeado **Trace_Oct_5_1.trc**, você pode renomear os arquivos a serem **TraceOct5.trc** e  **TraceOct5_1.trc**.  
  
 Essa função pode ler um rastreamento que ainda esteja ativo na instância na qual é executado.  
  
## <a name="permissions"></a>Permissões  
 Requer a permissão ALTER TRACE no servidor.  
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-using-fntracegettable-to-import-rows-from-a-trace-file"></a>A. Usando fn_trace_gettable para importar linhas de um arquivo de rastreamento  
 O exemplo a seguir chama `fn_trace_gettable` dentro da cláusula `FROM` de uma instrução `SELECT...INTO`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
### <a name="b-using-fntracegettable-to-return-a-table-with-an-identity-column-that-can-be-loaded-into-a-sql-server-table"></a>B. Usando fn_trace_gettable para retornar uma tabela com uma coluna IDENTITY que pode ser carregada em uma tabela do SQL Server  
 O exemplo a seguir chama a função como parte de uma instrução `SELECT...INTO` e retorna uma tabela com uma coluna `IDENTITY` que pode ser carregada na tabela `temp_trc`.  
  
```  
USE AdventureWorks2012;  
GO  
SELECT IDENTITY(int, 1, 1) AS RowNumber, * INTO temp_trc  
FROM fn_trace_gettable('c:\temp\mytrace.trc', default);  
GO  
```  
  
## <a name="see-also"></a>Consulte também  
 [sp_trace_generateevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-generateevent-transact-sql.md)   
 [sp_trace_setevent &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setevent-transact-sql.md)   
 [sp_trace_setfilter &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setfilter-transact-sql.md)   
 [sp_trace_setstatus &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-trace-setstatus-transact-sql.md)  
  
  
