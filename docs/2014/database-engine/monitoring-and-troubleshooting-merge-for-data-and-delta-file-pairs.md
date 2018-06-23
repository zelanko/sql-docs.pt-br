---
title: Monitorar e solucionar problemas de replicação de mesclagem para dados e Delta pares de arquivos | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine-imoltp
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: a8b0bacc-4d2c-42e4-84bf-1a97e0bd385b
caps.latest.revision: 12
author: stevestein
ms.author: sstein
manager: jhubbard
ms.openlocfilehash: 31c717aca9153ee851a35992ebdced9cea2d86c0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009206"
---
# <a name="monitoring-and-troubleshooting-merge-for-data-and-delta-file-pairs"></a>Monitorando e solucionando problemas de mesclagem de pares de arquivos delta e de dados
  O OLTP na memória usa uma política de mesclagem para mesclar automaticamente pares adjacentes de arquivos delta e de dados. Você não pode desabilitar a atividade de mesclagem.  
  
 Você pode monitorar pares de arquivos delta e de dados, da seguinte maneira:  
  
-   Compare o tamanho do armazenamento na memória ao tamanho geral do armazenamento. Se o armazenamento for desproporcionalmente grande, provavelmente a mesclagem não está sendo disparada. Para obter informações  
  
-   Examine o espaço usado nos arquivos delta e de dados usando [sys.DM db_xtp_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-dynamic-management-views/sys-dm-db-xtp-checkpoint-files-transact-sql) para ver se a mesclagem não está sendo disparada quando deveria.  
  
## <a name="performing-a-manual-merge"></a>Executando uma mesclagem manual  
 Você pode usar [sp_xtp_merge_checkpoint_files &#40;Transact-SQL&#41; ](/sql/relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql) para executar uma mesclagem manual.  
  
 Use a seguinte consulta para recuperar informações sobre os arquivos delta e de dados,  
  
```tsql  
select checkpoint_file_id, file_type_desc, internal_storage_slot, file_size_in_bytes, file_size_used_in_bytes,   
inserted_row_count, deleted_row_count, lower_bound_tsn, upper_bound_tsn   
from sys.dm_db_xtp_checkpoint_files  
where state = 1  
order by file_type_desc, upper_bound_tsn  
```  
  
 Suponha que você encontrou três arquivos de dados que não foram mesclados. Usando o valor de `lower_bound_tsn` do primeiro arquivo de dados e o valor de `upper_bound_tsn` do último arquivo de dados, você poderá emitir o seguinte comando:  
  
```tsql  
exec sys.sp_xtp_merge_checkpoint_files 'H_DB',  12345, 67890  
```  
  
 Suponha que os três pares de arquivos delta e de dados tinham 15.836 linhas e 5.279 linhas excluídas cada um. Após a mesclagem, o novo arquivo de dados tem 31.872 linhas e 0 linhas excluídas. O tamanho do novo arquivo de dados pode ser muito maior que o tamanho inicialmente alocado de 128 MB. Isso acontece porque a mesclagem manual substitui a política de mesclagem e força a mesclagem dos arquivos solicitados.  
  
 Blog do [estado de transição de ponto de verificação de arquivos em bancos de dados com tabelas com otimização de memória](http://blogs.technet.com/b/dataplatforminsider/archive/2014/01/23/state-transition-of-checkpoint-files-in-databases-with-memory-optimized-tables.aspx) descreve a transição de estado de pares de arquivos de dados e delta a do início à coleta de lixo.  
  
## <a name="see-also"></a>Consulte também  
 [Criando e gerenciando armazenamento para objetos com otimização de memória](../relational-databases/in-memory-oltp/creating-and-managing-storage-for-memory-optimized-objects.md)  
  
  
