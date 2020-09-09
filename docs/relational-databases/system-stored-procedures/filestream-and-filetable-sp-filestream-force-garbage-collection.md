---
description: sp_filestream_force_garbage_collection (Transact-SQL)
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
author: markingmyname
ms.author: maghan
ms.openlocfilehash: eeb70b4bc548496dcb8d0c93eeba27a9644c5bca
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89539180"
---
# <a name="sp_filestream_force_garbage_collection-transact-sql"></a>sp_filestream_force_garbage_collection (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Força a execução do coletor de lixo FILESTREAM, excluindo qualquer arquivo FILESTREAM desnecessário.  
  
 Não é possível remover um contêiner FILESTREAM antes que o coletor de lixo limpe todos os arquivos excluídos contidos nele. O coletor de lixo FILESTREAM é executado automaticamente. No entanto, se você precisar remover um contêiner antes da execução do coletor de lixo, poderá usar sp_filestream_force_garbage_collection para executar o coletor de lixo manualmente.  
  
  
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
> `@dbname` é **sysname**. Se não for especificado, o banco de dados atual será assumido.  
  
 `[ @filename = ] 'logical_file_name'`  
 Especifica o nome lógico do contêiner FILESTREAM no qual o coletor de lixo será executado. `@filename` é opcional. Se nenhum nome de arquivo lógico for especificado, o coletor de lixo limpará todos os contêineres FILESTREAM no banco de dados especificado.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
  
| Valor | Descrição |
| ----- | ----------- |   
|0|Êxito na operação|  
|1|Falha na operação|  
  
## <a name="result-sets"></a>Conjuntos de resultados  
  
|Valor|Descrição|  
|-----------|-----------------|  
|*file_name*|Indica o nome de contêiner FILESTREAM|  
|*num_collected_items*|Indica o número de itens FILESTREAM (arquivos/diretórios) que foram limpos (excluídos) pelo coletor de dados neste contêiner.|  
|*num_marked_for_collection_items*|Indica o número de itens FILESTREAM (arquivos/diretórios) que foram marcados para coleta de lixo neste contêiner. Esses itens ainda não foram excluídos, mas podem estar qualificados para exclusão após a fase de coleta de lixo.|  
|*num_unprocessed_items*|Indica o número de itens FILESTREAM qualificados (arquivos ou diretórios) que não foram processados para coleta de lixo neste FILESTREAM. Itens podem não ser processados por várias razões, inclusive as seguintes:<br /><br /> Arquivos que precisam ser definidos porque não foi obtido o backup de log ou um ponto de verificação.<br /><br /> Arquivos no modelo de recuperação FULL ou BULK_LOGGED.<br /><br /> Há uma transação ativa de execução longa.<br /><br /> O trabalho do leitor de log de replicação não foi executado. Consulte o white paper [armazenamento FileStream no SQL Server 2008](https://go.microsoft.com/fwlink/?LinkId=209156) para obter mais informações.|  
|*last_collected_xact_seqno*|Retorna o número de sequência de log correspondente (LSN) até onde os arquivos do contêiner FILESTREAM especificado foram coletados pelo coletor de lixo.|  
  
## <a name="remarks"></a>Comentários  
 Executa explicitamente a tarefa Coletor de lixo FILESTREAM até a conclusão no banco de dados solicitado (e no contêiner FILESTREAM). Arquivos que não são mais necessários são removidos pelo processo de coleta de lixo. O tempo necessário para que essa operação seja concluída depende do tamanho dos dados FILESTREAM no banco de dados ou contêiner, bem como a quantidade de atividades de DML ocorridas recentemente nos dados FILESTREAM. Embora esta operação possa ser executada com o banco de dados online, isso pode afetar o desempenho do banco de dados durante sua execução devido a várias atividades de E/S feitas pelo processo de coleta de lixo.  
  
> [!NOTE]  
>  É recomendado que esta operação apenas seja executada quando necessário e fora de horas de operação habituais.  
  
É possível executar várias invocações desse procedimento armazenado simultaneamente em contêineres ou em bancos de dados separados.  

Devido a operações de duas fases, o procedimento armazenado deve ser executado duas vezes para realmente excluir arquivos FILESTREAM subjacentes.  

A coleta de lixo (GC) depende do truncamento de log. Portanto, se os arquivos foram excluídos recentemente em um banco de dados usando o modelo de recuperação completa, eles são GC-Ed somente depois que um backup de log dessas partes de log de transações é obtido e a parte de log é marcada como inativa. Em um banco de dados que usa um modelo de recuperação simples, um truncamento de log ocorre depois `CHECKPOINT` que um é emitido no banco de dados.  


## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados db_owner.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos a seguir executam o coletor de lixo para contêineres FILESTREAM no banco de dados `FSDB`.  
  
### <a name="a-specifying-no-container"></a>a. Não especificando nenhum contêiner  
  
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
  
## <a name="see-also"></a>Consulte Também  
[Fluxo de arquivos](../../relational-databases/blob/filestream-sql-server.md)
<br>[Filetables](../../relational-databases/blob/filetables-sql-server.md)
<br>[Exibições de gerenciamento dinâmico de fluxo de arquivos e FileTable (Transact-SQL)](../system-dynamic-management-views/filestream-and-filetable-dynamic-management-views-transact-sql.md)
<br>[Exibições de catálogo de fluxo de arquivos e FileTable (Transact-SQL)](../system-catalog-views/filestream-and-filetable-catalog-views-transact-sql.md)
<br>[sp_kill_filestream_non_transacted_handles (Transact-SQL)](filestream-and-filetable-sp-kill-filestream-non-transacted-handles.md)
  
  
