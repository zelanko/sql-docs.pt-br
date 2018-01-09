---
title: Atualizando dados em cursores do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-ole-db-rowsets
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: fc0073e33de3256859540002bb6a356e731238de
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Ao buscar e atualizar dados por meio de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo consumidor do provedor de OLE DB Native Client é associado pelas mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client oferece suporte ao isolamento de leitura suja quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediata, cada chamada para **IRowsetChange:: SetData** causa uma viagem para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações a uma única linha, é mais eficiente enviar todas as alterações com um único **SetData** chamar.  
  
 No modo de atualização com atraso, uma ida e volta é feita para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada linha indicada no *cRows* e *rghRows* parâmetros de **IRowsetUpdate:: Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Quando você estiver usando **IRowsetUpdate:: Update**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client tenta processar cada linha indicada. Um erro que ocorre devido a valores inválidos de dados, o tamanho ou o status para qualquer linha não interrompe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processamento do provedor OLE DB Native Client. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor deve examinar retornado *prgRowStatus* matriz para determinar a falha para qualquer específica de linha quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client retorna DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando dados em conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/updating-data-in-rowsets.md)  
  
  
