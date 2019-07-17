---
title: suspect_pages (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 06/10/2016
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- suspect_page_table
- suspect_page_table_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- suspect_pages system table
- suspect pages [SQL Server]
ms.assetid: 119c8d62-eea8-44fb-bf72-de469c838c50
author: stevestein
ms.author: sstein
ms.openlocfilehash: 70dffcbf2ac3eac13f7ef42e901c4fcd99dce769
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68130546"
---
# <a name="suspectpages-transact-sql"></a>suspect_pages (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]

  Contém uma linha por página que falhou com um erro 823 secundário ou um erro 824. As páginas são relacionadas nesta tabela porque há suspeita de que sejam inadequadas, mas pode ser que de fato estejam adequadas. Quando uma página suspeita for reparada, seu status é atualizado na **event_type** coluna.  
  
 A tabela a seguir, que tem um limite de 1.000 linhas, é armazenada na **msdb** banco de dados.  
  
|Nome da coluna|Tipo de dados|Descrição|  
|-----------------|---------------|-----------------|  
|**database_id**|**int**|ID do banco de dados ao qual esta página se aplica.|  
|**file_id**|**int**|ID do arquivo no banco de dados.|  
|**page_id**|**bigint**|ID da página suspeita. Cada página tem uma identificação de página que é um valor de 32 bits que identifica o local da página no banco de dados. O **page_id** é o deslocamento no arquivo de dados da página de 8 KB. Cada ID de página é exclusivo em um arquivo.|  
|**event_type**|**int**|O tipo de erro; um de:<br /><br /> 1 = Um erro 823 que causa uma página suspeita (como um erro de disco) ou um erro 824, exceto uma soma de verificação inválida ou uma página interrompida (como uma ID de página inválida).<br /><br /> 2 = Soma de verificação inválida.<br /><br /> 3 = Página interrompida.<br /><br /> 4 = Restaurada (a página foi restaurada depois de marcada como inválida).<br /><br /> 5 = Reparada (DBCC reparou a página).<br /><br /> 7 = Desalocada pelo DBCC.|  
|**error_count**|**int**|Número de vezes em que o erro ocorreu.|  
|**last_update_date**|**datetime**|Carimbo de data/hora da última atualização.|  
  
## <a name="permissions"></a>Permissões  
 Qualquer pessoa com acesso ao **msdb** pode ler os dados na tabela **suspect_pages** . Qualquer um com permissão UPDATE na tabela suspect_pages pode atualizar seus registros. Os membros da função de banco de dados fixa **db_owner** no **msdb** ou da função de servidor fixa **sysadmin** podem inserir, atualizar e excluir registros.  
  
## <a name="see-also"></a>Consulte também  
 [Restaurar páginas &#40;SQL Server&#41;](../../relational-databases/backup-restore/restore-pages-sql-server.md)   
 [Classe de evento de página de dados suspeito de banco de dados](../../relational-databases/event-classes/database-suspect-data-page-event-class.md)   
 [Tabelas do sistema &#40;Transact-SQL&#41;](../../relational-databases/system-tables/system-tables-transact-sql.md)   
 [Gerenciar a tabela suspect_pages &#40;SQL Server&#41;](../../relational-databases/backup-restore/manage-the-suspect-pages-table-sql-server.md)  
  
  
