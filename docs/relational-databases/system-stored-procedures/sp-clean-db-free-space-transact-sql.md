---
title: sp_clean_db_free_space (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_clean_db_free_space_TSQL
- sp_clean_db_free_space
dev_langs:
- TSQL
helpviewer_keywords:
- sp_clean_db_free_space
- ghost records
ms.assetid: faa96f7e-be92-47b1-8bc5-4dbba5331655
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: cf21502e06d67edd2e9d5c3dcfdd3c5caa42704c
ms.sourcegitcommit: 4d3896882c5930248a6e441937c50e8e027d29fd
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/05/2020
ms.locfileid: "82823997"
---
# <a name="sp_clean_db_free_space-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove informações residuais deixadas em páginas de banco de dados devido a rotinas de modificação de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_free_space limpa todas as páginas em todos os arquivos do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_clean_db_free_space   
[ @dbname ] = 'database_name'   
[ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname =] '*database_name*'  
 É o nome do banco de dados a ser limpo. *dbname* é **sysname** e não pode ser nulo.  
  
 [ @cleaning_delay =] '*delay_in_seconds*'  
 Especifica um intervalo de atraso entre a limpeza das páginas. Isso ajuda a reduzir o efeito no sistema de E/S. *delay_in_seconds* é **int** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 As operações de exclusão de uma tabela ou as operações de atualização que fazem com que uma linha seja movida podem liberar espaço imediatamente em uma página removendo as referências para a linha. No entanto, em certas circunstâncias, a linha pode permanecer fisicamente na página de dados como um registro fantasma. Os registros fantasmas são removidos periodicamente por um processo em segundo plano. Esses dados residuais não são retornados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] em resposta a consultas. Entretanto, em ambientes nos quais a segurança física dos dados ou arquivos de backup está em risco, você pode usar sp_clean_db_free_space para limpar esses registros fantasmas.  
  
 O período de tempo necessário para a execução de sp_clean_db_free_space depende do tamanho do arquivo, do espaço livre disponível e da capacidade do disco. Como a execução de sp_clean_db_free_space pode afetar significativamente a atividade de E/S, é recomendável executar esse procedimento fora do horário de operação normal.  
  
 Antes da execução de sp_clean_db_free_space, é recomendável criar um backup completo do banco de dados.  
  
 O procedimento armazenado [sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) relacionado pode limpar um único arquivo.  
  
## <a name="permissions"></a>Permissões  
 Requer associação na função de banco de dados db_owner.  
  
## <a name="examples"></a>Exemplos  
 O exemplo a seguir limpa todas as informações residuais do banco de dados `AdventureWorks2012`.  
  
```  
USE master;  
GO  
EXEC sp_clean_db_free_space   
@dbname = N'AdventureWorks2012' ;  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Mecanismo de Banco de Dados procedimentos armazenados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)
 <br>[Guia de processo de limpeza de fantasma](../ghost-record-cleanup-process-guide.md) 
  
  
