---
title: sp_clean_db_free_space (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.service: ''
ms.component: system-stored-procedures
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
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
caps.latest.revision: 12
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 44e07452d0b9d8b53906a810005d11ed0a801665
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="spcleandbfreespace-transact-sql"></a>sp_clean_db_free_space (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Remove informações residuais deixadas em páginas de banco de dados devido a rotinas de modificação de dados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. sp_clean_db_free_space limpa todas as páginas em todos os arquivos do banco de dados.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_clean_db_free_space   
[ @dbname ] = 'database_name'   
[ , [ @cleaning_delay = ] 'delay_in_seconds' ] [;]  
```  
  
## <a name="arguments"></a>Argumentos  
 [ @dbname=] '*database_name*'  
 É o nome do banco de dados a ser limpo. *DBName* é **sysname** e não pode ser NULL.  
  
 [ @cleaning_delay=] '*atraso_em_segundos*'  
 Especifica um intervalo de atraso entre a limpeza das páginas. Isso ajuda a reduzir o efeito no sistema de E/S. *atraso_em_segundos* é **int** com um padrão de 0.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Remarks  
 As operações de exclusão de uma tabela ou as operações de atualização que fazem com que uma linha seja movida podem liberar espaço imediatamente em uma página removendo as referências para a linha. No entanto, em certas circunstâncias, a linha pode permanecer fisicamente na página de dados como um registro fantasma. Os registros fantasmas são removidos periodicamente por um processo em segundo plano. Esses dados residuais não são retornados pelo [!INCLUDE[ssDE](../../includes/ssde-md.md)] em resposta a consultas. Entretanto, em ambientes nos quais a segurança física dos dados ou arquivos de backup está em risco, você pode usar sp_clean_db_free_space para limpar esses registros fantasmas.  
  
 O período de tempo necessário para a execução de sp_clean_db_free_space depende do tamanho do arquivo, do espaço livre disponível e da capacidade do disco. Como a execução de sp_clean_db_free_space pode afetar significativamente a atividade de E/S, é recomendável executar esse procedimento fora do horário de operação normal.  
  
 Antes da execução de sp_clean_db_free_space, é recomendável criar um backup completo do banco de dados.  
  
 Relacionado [sp_clean_db_file_free_space](../../relational-databases/system-stored-procedures/sp-clean-db-file-free-space-transact-sql.md) procedimento armazenado pode limpar um único arquivo.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados do mecanismo de banco de dados &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/database-engine-stored-procedures-transact-sql.md)  
  
  
