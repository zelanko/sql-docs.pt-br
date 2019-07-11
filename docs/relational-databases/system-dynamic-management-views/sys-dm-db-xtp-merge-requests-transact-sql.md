---
title: sys.dm_db_xtp_merge_requests (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 02/01/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
ms.assetid: c1224e88-af74-4c99-ae32-d5d2c552a1f5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1c7ff8638aeeb02cdb86643fd1fc6a3241a8db26
ms.sourcegitcommit: e0c55d919ff9cec233a7a14e72ba16799f4505b2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/10/2019
ms.locfileid: "67732544"
---
# <a name="sysdmdbxtpmergerequests-transact-sql"></a>sys.dm_db_xtp_merge_requests (Transact-SQL)

[!INCLUDE[tsql-appliesto-ss2014-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2014-xxxx-xxxx-xxx-md.md)]

Rastreia solicitações de mesclagem de banco de dados. A solicitação de mesclagem pode ter sido gerada pelo SQL Server ou a solicitação foi feita por um usuário com [sp_xtp_merge_checkpoint_files (Transact-SQL)](../../relational-databases/system-stored-procedures/sys-sp-xtp-merge-checkpoint-files-transact-sql.md).

> [!NOTE]
> Este modo de exibição de gerenciamento dinâmico (DMV), sys.dm_db_xtp_merge_requests, existe até o Microsoft SQL Server 2014.
> Mas, começando com o SQL Server 2016, essa DMV não se aplica.

## <a name="columns-in-the-report"></a>Colunas do relatório

| Nome da coluna | Tipo de dados | Descrição |
| :-- | :-- | :-- |
| request_state | TINYINT | O status da solicitação de mesclagem:<br/>0 = solicitado<br/>1 = pendente<br/>2 = instalado<br/>3 = abandonado |
| request_state_desc | nvarchar(60) | Significados para o estado atual da solicitação:<br/><br/>Uma solicitação de mesclagem solicitado - existe.<br/>Pendente - a mesclagem está sendo processada.<br/>Instalado - a mesclagem foi concluída.<br/>Abandonado - a mesclagem não pôde concluir, talvez devido à falta de armazenamento. |
| destination_file_id | GUID | O identificador exclusivo do arquivo de destino para a mesclagem dos arquivos de origem. |
| lower_bound_tsn | BIGINT | O carimbo de data/hora mínimo para o arquivo de mesclagem de destino. O carimbo de data/hora da transação mais baixa de todos os arquivos de origem a serem mesclados. |
| upper_bound_tsn | BIGINT | O carimbo de data/hora máximo para o arquivo de mesclagem de destino. O carimbo de data/hora da transação mais alta de todos os arquivos de origem a serem mesclados. |
| collection_tsn | BIGINT | O carimbo de data/hora em que a linha atual pode ser coletada.<br/><br/>Uma linha no estado Instalado será removida quando checkpoint_tsn for maior que collection_tsn.<br/><br/>Uma linha no estado Abandonado será removida quando checkpoint_tsn for menor que collection_tsn. |
| checkpoint_tsn | BIGINT | A hora em que o ponto de verificação foi iniciado.<br/><br/>Todas as exclusões feitas por transações com um carimbo de data/hora inferior a esse serão contabilizadas no novo arquivo de dados. As exclusões restantes são movidas para o arquivo delta de destino. |
| sourcenumber_file_id | GUID | Até 16 IDs internas do arquivo que identificam exclusivamente os arquivos de origem na mesclagem. |

## <a name="permissions"></a>Permissões

Requer a permissão VIEW DATABASE STATE no banco de dados atual.

## <a name="see-also"></a>Confira também

[Exibições de gerenciamento dinâmico de tabela com otimização de memória (Transact-SQL)](../../relational-databases/system-dynamic-management-views/memory-optimized-table-dynamic-management-views-transact-sql.md)
