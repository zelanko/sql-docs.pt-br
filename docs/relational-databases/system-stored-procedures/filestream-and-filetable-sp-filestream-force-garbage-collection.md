---
title: sp_filestream_force_garbage_collection (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 07/22/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_filestream_force_garbage_collection
- sp_filestream_force_garbage_collection_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- FILESTREAM [SQL Server]
- sp_filestream_force_garbage_collection
ms.assetid: 9d1efde6-8fa4-42ac-80e5-37456ffebd0b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: c8f202dd4f383d1ed2186e589b275afc0049fb50
ms.sourcegitcommit: acb5de9f493238180d13baa302552fdcc30d83c0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/12/2019
ms.locfileid: "59542206"
---
# <a name="spfilestreamforcegarbagecollection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-xxxx-xxxx-xxx-md.md)]

  Força a execução do coletor de lixo FILESTREAM, excluindo qualquer arquivo FILESTREAM desnecessário.  
  
 Não é possível remover um contêiner FILESTREAM antes que o coletor de lixo limpe todos os arquivos excluídos contidos nele. O coletor de lixo FILESTREAM é executado automaticamente. No entanto, se você precisar remover um contêiner antes do coletor de lixo foi executada, você pode usar sp_filestream_force_garbage_collection para executar o coletor de lixo manualmente.  
  
  
## <a name="syntax"></a>Sintaxe  
  
```  
sp_filestream_force_garbage_collection
    [ @dbname = ]  'database_name'
    [ , [ @filename = ] 'logical_file_name' ]
```  
  
## <a name="arguments"></a>Argumentos  
 `[ @dbname = ]  'database_name'`  
 Significa o nome do banco de dados no qual o coletor de lixo será executado.  
  
> [!NOTE]  
> `@dbname` está **sysname**. Se não for especificado, o atual banco de dados será assumido.  
  
 `[ @filename = ] 'logical_file_name'`  
 Especifica o nome lógico do contêiner FILESTREAM no qual o coletor de lixo será executado. `@filename` é opcional. Se nenhum nome de arquivo lógico for especificado, o coletor de lixo limpa todos os contêineres FILESTREAM no banco de dados especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
  
|||  
|-|-|  
|Valor|Descrição|  
|0|Êxito na operação|  
|1|Falha na operação|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*file_name*|Indica o nome de contêiner FILESTREAM|  
|*num_collected_items*|Indica o número de itens FILESTREAM (arquivos/diretórios) que foram limpos (excluídos) pelo coletor de dados neste contêiner.|  
|*num_marked_for_collection_items*|Indica o número de itens FILESTREAM (arquivos/diretórios) que foram marcados para coleta de lixo neste contêiner. Estes itens ainda não foram excluídos, mas podem ser elegíveis para exclusão após a fase de coleta de lixo.|  
|*num_unprocessed_items*|Indica o número de itens FILESTREAM qualificados (arquivos ou diretórios) que não foram processados para coleta de lixo neste FILESTREAM. Itens podem não ser processados por várias razões, inclusive as seguintes:<br /><br /> Arquivos que precisam ser definidos porque não foi obtido o backup de log ou um ponto de verificação.<br /><br /> Arquivos no modelo de recuperação FULL ou BULK_LOGGED.<br /><br /> Há uma transação ativa de execução longa.<br /><br /> O trabalho de leitor de log de replicação não foi executada. Consulte o white paper [armazenamento de FILESTREAM no SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=209156) para obter mais informações.|  
|*last_collected_xact_seqno*|Retorna o número de sequência de log correspondente (LSN) até onde os arquivos do contêiner FILESTREAM especificado foram coletados pelo coletor de lixo.|  
  
## <a name="remarks"></a>Comentários  
 Executa explicitamente a tarefa Coletor de lixo FILESTREAM até a conclusão no banco de dados solicitado (e no contêiner FILESTREAM). Arquivos que não são mais necessários são removidos pelo processo de coleta de lixo. O tempo necessário para que essa operação seja concluída depende do tamanho dos dados FILESTREAM no banco de dados ou contêiner, bem como a quantidade de atividades de DML ocorridas recentemente nos dados FILESTREAM. Embora esta operação possa ser executada com o banco de dados online, isso pode afetar o desempenho do banco de dados durante sua execução devido a várias atividades de E/S feitas pelo processo de coleta de lixo.  
  
> [!NOTE]  
>  É recomendado que esta operação apenas seja executada quando necessário e fora de horas de operação habituais.  
  
É possível executar várias invocações desse procedimento armazenado simultaneamente em contêineres ou em bancos de dados separados.  

Devido a operações de fase 2, o procedimento armazenado deve ser executado duas vezes para realmente excluir os arquivos de Filestream subjacentes.  

Coleta de lixo (GC) se baseia em truncamento de log. Portanto, se os arquivos foram excluídos recentemente em um banco de dados usando o modelo de recuperação completa, eles são GC ed somente depois que é feito um backup de log dessas partes do log de transação e a parte do log é marcada como inativa. Em um banco de dados usando o modelo de recuperação simples, ocorre um truncamento de log após um `CHECKPOINT` tiver sido emitida no banco de dados.  


## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados db_owner.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir executam o coletor de lixo para contêineres FILESTREAM no banco de dados `FSDB`.  
  
### <a name="a-specifying-no-container"></a>A. Não especificando nenhum contêiner  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB';  
```  
  
### <a name="b-specifying-a-container"></a>B. Especificando um contêiner  
  
```sql  
USE FSDB;  
GO  
EXEC sp_filestream_force_garbage_collection @dbname = N'FSDB',
    @filename = N'FSContainer';  
```  
  
## <a name="see-also"></a>Consulte também  
[Filestream](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
