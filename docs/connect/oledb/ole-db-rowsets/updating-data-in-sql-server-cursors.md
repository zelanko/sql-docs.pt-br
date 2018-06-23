---
title: Atualizando dados em cursores do SQL Server | Microsoft Docs
description: Atualizando dados em cursores do SQL Server
ms.custom: ''
ms.date: 06/14/2018
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: oledb|ole-db-rowsets
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
author: pmasl
ms.author: Pedro.Lopes
manager: craigg
ms.openlocfilehash: 8cece02b19e2334246dbddc096cafbeeae705684
ms.sourcegitcommit: 03ba89937daeab08aa410eb03a52f1e0d212b44f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/16/2018
ms.locfileid: "35689499"
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-asdbmi-md](../../../includes/appliesto-ss-asdb-asdw-pdw-asdbmi-md.md)]

[!INCLUDE[Driver_OLEDB_Download](../../../includes/driver_oledb_download.md)]

  Ao buscar e atualizar dados por meio de [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] cursores, um Driver OLE DB para o aplicativo do consumidor vinculado, as mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente do SQL Server.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o Driver OLE DB para SQL Server usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O Driver OLE DB para SQL Server dá suporte ao isolamento de leitura suja quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediata, cada chamada para **IRowsetChange:: SetData** causa uma viagem para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações a uma única linha, é mais eficiente enviar todas as alterações com um único **SetData** chamar.  
  
 No modo de atualização com atraso, uma ida e volta é feita para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] para cada linha indicada no *cRows* e *rghRows* parâmetros de **IRowsetUpdate:: Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Quando você estiver usando **IRowsetUpdate:: Update**, o Driver OLE DB para SQL Server tenta processar cada linha indicada. Um erro que ocorre devido a valores inválidos de dados, o tamanho ou o status para qualquer linha não interrompe o Driver do OLE DB para processamento do SQL Server. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor deve examinar retornado *prgRowStatus* matriz para determinar a falha de qualquer linha específica quando o Driver OLE DB para SQL Server retorna DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando dados em conjuntos de linhas](../../oledb/ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
