---
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
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: 4b8c7157eac444815eae0b4846519b93389be2f4
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85771316"
---
# <a name="sp_clean_db_file_free_space-transact-sql"></a>sp_clean_db_file_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/applies-to-version/sqlserver.md)]

  Remove informações residuais deixadas em páginas de banco de dados devido a rotinas de modificação de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_file_free_space limpa todas as páginas em só um arquivo de um banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_clean_db_file_free_space   
[ @dbname ] = 'database_name'   
, @fileid = 'file_number'   
 [ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname =] '*database_name*'  
 É o nome do banco de dados a ser limpo. *dbname* é **sysname** e não pode ser nulo.  
  
 [ @fileid =] '*file_number*'  
 É a ID de arquivo de dados a ser limpa. *file_number* é **int** e não pode ser NULL.  
  
 [ @cleaning_delay =] '*delay_in_seconds*'  
 Especifica um intervalo de atraso entre a limpeza das páginas. Isso ajuda a reduzir o efeito no sistema de E/S. *delay_in_seconds* é **int** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 As operações de exclusão de uma tabela ou as operações de atualização que fazem com que uma linha seja movida podem liberar espaço imediatamente em uma página por meio da remoção das referências à linha. No entanto, em certas circunstâncias, a linha pode permanecer fisicamente na página de dados como um registro fantasma. Os registros fantasmas são removidos periodicamente por um processo em segundo plano. Esses dados residuais não são retornados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] em resposta a consultas. Entretanto, em ambientes nos quais a segurança física dos dados ou arquivos de backup está em risco, você pode usar sp_clean_db_file_free_space para limpar esses registros fantasmas.  
  
 O período de tempo necessário para a execução de sp_clean_db_file_free_space depende do tamanho do arquivo, do espaço livre disponível e da capacidade do disco. Como a execução de sp_clean_db_file_free_space pode afetar significativamente a atividade de E/S, é recomendável executar esse procedimento fora do horário de operação normal.  
  
 Antes da execução de sp_clean_db_file_free_space, é recomendável criar um backup completo do banco de dados.  
  
 O procedimento armazenado [sp_clean_db_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-free-space-transact-sql.md) relacionado limpa todos os arquivos no banco de dados.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados db_owner.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir limpa todas as informações residuais do arquivo de dados primário do banco de dados `AdventureWorks2012`.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_file_free_space   
@dbname = N'AdventureWorks2012', @fileid = 1 ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)
 <br>[Guia de processo de limpeza de fantasma](../ghost-record-cleanup-process-guide.md) 
  
  
