---
description: sp_clean_db_file_free_space (Transact-SQL)
title: sp_clean_db_file_free_space (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_clean_db_file_free_space
- sp_clean_db_file_free_space_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- ghost records
- sp_clean_db_file_free_space
ms.assetid: 3eb53a67-969d-4cb8-9681-b1c8e6fd55b6
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 75463e5785c76e6904d2d7a82bf03f160811e6d0
ms.sourcegitcommit: dd36d1cbe32cd5a65c6638e8f252b0bd8145e165
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/08/2020
ms.locfileid: "89543611"
---
# <a name="sp_clean_db_file_free_space-transact-sql"></a>sp_clean_db_file_free_space (Transact-SQL)
[!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]

  Remove informações residuais deixadas em páginas de banco de dados devido a rotinas de modificação de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_file_free_space limpa todas as páginas em só um arquivo de um banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```syntaxsql  
sp_clean_db_file_free_space   
  [ @dbname = ] 'database_name'   
  , [ @fileid = ] 'file_number'   
  [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 @dbname = '*database_name*'  
 É o nome do banco de dados a ser limpo. *dbname* é **sysname** e não pode ser nulo.  
  
 @fileid = '*file_number*'  
 É a ID de arquivo de dados a ser limpa. *file_number* é **int** e não pode ser NULL.  
  
 @cleaning_delay = '*delay_in_seconds*'  
 Especifica um intervalo de atraso entre a limpeza das páginas. Isso ajuda a reduzir o efeito no sistema de E/S. *delay_in_seconds* é **int** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 As operações de exclusão de uma tabela ou as operações de atualização que fazem com que uma linha seja movida podem liberar espaço imediatamente em uma página por meio da remoção das referências à linha. No entanto, em certas circunstâncias, a linha pode permanecer fisicamente na página de dados como um registro fantasma. Os registros fantasmas são removidos periodicamente por um processo em segundo plano. Esses dados residuais não são retornados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] em resposta a consultas. No entanto, em ambientes nos quais a segurança física dos arquivos de dados ou de backup está em risco, você pode usar o `sp_clean_db_file_free_space` para limpar esses registros fantasma. Para executar essa operação para todos os arquivos de banco de dados ao mesmo tempo, use [sp_clean_db_free_space (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md). 
  
 O período de tempo necessário para a execução de sp_clean_db_file_free_space depende do tamanho do arquivo, do espaço livre disponível e da capacidade do disco. Como `sp_clean_db_file_free_space` a execução pode afetar significativamente a atividade de e/s, recomendamos que você execute esse procedimento fora do horário de operação usual.  
  
 Antes de executar `sp_clean_db_file_free_space` o, recomendamos que você crie um backup de banco de dados completo.  
  
 O procedimento armazenado [sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md) relacionado limpa todos os arquivos no banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na `db_owner` função de banco de dados.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir limpa todas as informações residuais do arquivo de dados primário do banco de dados `AdventureWorks2012`.  
  
```sql  
USE master;  
GO  
EXEC sp_clean_db_file_free_space @dbname = N'AdventureWorks2012', @fileid = 1;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)   
 [Guia de processo de limpeza de fantasma](../ghost-record-cleanup-process-guide.md)    
 [sp_clean_db_free_space (Transact-SQL)](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md)
   
