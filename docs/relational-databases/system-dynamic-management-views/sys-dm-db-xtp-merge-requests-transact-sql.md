---
title: sys. dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: CarlRabeler
ms.author: carlrab
ms.openlocfilehash: f489b01655f3b6836c1360bc0e473747e62ca59e
ms.sourcegitcommit: 039fb38c583019b3fd06894160568387a19ba04e
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/30/2020
ms.locfileid: "87442669"
---
# <a name="sysdm_db_xtp_merge_requests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[sqlserver](../../includes/applies-to-version/sqlserver.md)]

Rastreia solicitações de mesclagem de banco de dados. A solicitação de mesclagem pode ter sido gerada por SQL Server ou a solicitação pode ter sido feita por um usuário com [Sys. sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Essa DMV (exibição de gerenciamento dinâmico), sys. dm_db_xtp_merge_requests, existe até Microsoft SQL Server 2014.
> Mas, a partir do SQL Server 2016, essa DMV não se aplica mais.

## <a name="columns-in-the-report"></a>Colunas no relatório

| Nome da coluna | Tipo de dados | Descrição |
| :-- | :-- | :-- |
| request_state | TINYINT | O status da solicitação de mesclagem:<br/>0 = solicitado<br/>1 = pendente<br/>2 = instalado<br/>3 = abandonado |
| request_state_desc | nvarchar(60) | Significas para o estado atual da solicitação:<br/><br/>Solicitado-existe uma solicitação de mesclagem.<br/>Pendente-a mesclagem está sendo processada.<br/>Instalado-a mesclagem foi concluída.<br/>Abandonado-a mesclagem não pôde ser concluída, talvez devido à falta de armazenamento. |
| destination_file_id | GUID | O identificador exclusivo do arquivo de destino para a mesclagem dos arquivos de origem. |
| lower_bound_tsn | BIGINT | O carimbo de data/hora mínimo para o arquivo de mesclagem de destino. O carimbo de data/hora da transação mais baixa de todos os arquivos de origem a serem mesclados. |
| upper_bound_tsn | BIGINT | O carimbo de data/hora máximo para o arquivo de mesclagem de destino. O carimbo de data/hora da transação mais alta de todos os arquivos de origem a serem mesclados. |
| collection_tsn | BIGINT | O carimbo de data/hora em que a linha atual pode ser coletada.<br/><br/>Uma linha no estado Instalado será removida quando checkpoint_tsn for maior que collection_tsn.<br/><br/>Uma linha no estado Abandonado será removida quando checkpoint_tsn for menor que collection_tsn. |
| checkpoint_tsn | BIGINT | A hora em que o ponto de verificação foi iniciado.<br/><br/>Todas as exclusões feitas por transações com um carimbo de data/hora inferior a esse serão contabilizadas no novo arquivo de dados. As exclusões restantes são movidas para o arquivo delta de destino. |
| sourcenumber_file_id | GUID | Até 16 IDs de arquivo interno que identificam exclusivamente os arquivos de origem na mesclagem. |

## <a name="permissions"></a>Permissões

Requer a permissão VIEW DATABASE STATE no banco de dados atual.

## <a name="see-also"></a>Veja também

[Exibições de gerenciamento dinâmico da tabela com otimização de memória (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
