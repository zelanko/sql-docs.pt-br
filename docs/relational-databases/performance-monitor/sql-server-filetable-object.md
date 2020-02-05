---
title: SQL Server, objeto FileTable | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: performance
ms.topic: conceptual
helpviewer_keywords:
- SQLServer:FileTable
ms.assetid: 325f5e58-1095-450f-9321-dfacfe6fd55f
author: julieMSFT
ms.author: jrasnick
ms.openlocfilehash: f2110726db47cf76adffca4b10f153ce941565cc
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "68093501"
---
# <a name="sql-server-filetable-object"></a>SQL Server, objeto FileTable
[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md](../../includes/appliesto-ss-xxxx-xxxx-xxx-md.md)]
O objeto de desempenho **SQLServer:FileTable** fornece contadores para estatísticas associadas a FileTable e ao acesso não transacionado.

A tabela a seguir descreve os objetos de desempenho **FileTable** do SQL Server.

|**Contadores de FileTable do SQL Server**|DESCRIÇÃO|  
|-------------|-----------------|  
|**Tempo médio para excluir um item FileTable**|Tempo médio (em milissegundos) para excluir um item FileTable.|
|**Tempo médio de enumeração de FileTable**|Tempo médio (em milissegundos) de uma solicitação de enumeração FileTable.|
|**Tempo médio de encerramento de identificador FileTable**|Tempo médio (em milissegundos) para encerrar um identificador FileTable.|
|**Tempo médio para mover um item FileTable**|Tempo médio (em milissegundos) para mover um item FileTable.|
|**Tempo médio por solicitação de E/S de arquivo**|Tempo médio (em milissegundos) gasto no tratamento de uma solicitação de E/S de arquivo de entrada.|
|**Tempo médio por resposta de E/S de arquivo**|Tempo médio (em milissegundos) gasto no tratamento de uma resposta de E/S de arquivo de saída.|
|**Tempo médio para renomear um item FileTable**|Tempo médio (em milissegundos) para renomear um item FileTable.|
|**Tempo médio para obter um item FileTable**|Tempo médio (em milissegundos) para recuperar um item FileTable.|
|**Tempo médio para atualizar um item FileTable**|Tempo médio (em milissegundos) para atualizar um item FileTable.|
|**Operações de banco de dados de FileTable/s**|Número total de eventos operacionais do banco de dados processados pelo componente de repositório FileTable por segundo.|
|**Solicitações de enumeração de FileTable/s**|Número total de solicitações de enumeração FileTable por segundo.|
|**Solicitações de E/S de arquivo FileTable/s**|Número total de solicitações de E/S de arquivo FileTable de entrada por segundo.|
|**Resposta de E/S de arquivo FileTable/s**|Número total de respostas de E/S de arquivo de saída por segundo.|
|**Solicitações de exclusão de item FileTable/s**|Número total de solicitações de exclusão de item FileTable por segundo.|
|**Solicitações de obtenção de um item FileTable/s**|Número total de solicitações de recuperação de item FileTable por segundo.|
|**Solicitações de movimentação de item FileTable/s**|Número total de solicitações de movimentação de item FileTable por segundo.|
|**Solicitações de renomeação de item FileTable/s**|Número total de solicitações de renomeação de item FileTable por segundo.|
|**Solicitações de atualização de item FileTable/s**|Número total de solicitações de atualização de item FileTable por segundo.|
|**Ops. de encerramento de identificador FileTable/s**|Número total de operações de encerramento de identificador FileTable por segundo.|
|**Operações de tabela FileTable/s**|Número total de eventos operacionais de tabela processados pelo componente de repositório FileTable por segundo.|
|**Tempo para excluir um item FileTable BASE**|Apenas para uso interno.|
|**Tempo de enumeração de FileTable BASE**|Apenas para uso interno.|
|**Tempo de encerramento de identificador FileTable BASE**|Apenas para uso interno.|
|**Tempo para mover um item FileTable BASE**|Apenas para uso interno.|
|**Tempo por solicitação de E/S de arquivo BASE**|Apenas para uso interno.|
|**Tempo por resposta de E/S de arquivo BASE**|Apenas para uso interno.|
|**Tempo para renomear um item FileTable BASE**|Apenas para uso interno.|
|**Tempo para obter um item FileTable BASE**|Apenas para uso interno.|
|**Tempo para atualizar um item FileTable BASE**|Apenas para uso interno.| 
 
## <a name="see-also"></a>Consulte Também  
[Monitorar o uso de recursos (Monitor do Sistema)](../../relational-databases/performance-monitor/monitor-resource-usage-system-monitor.md)
