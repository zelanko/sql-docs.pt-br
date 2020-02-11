---
title: Atualizando dados em cursores SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b5c0b188d8fd45c1177cab77501bdf80fc550987
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63242916"
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
  Ao buscar e atualizar dados por meio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de cursores, [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] um aplicativo de consumidor de provedor de OLE DB de cliente nativo é associado pelas mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo dá suporte ao isolamento de leitura sujo quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediato, cada chamada a **IRowsetChange::SetData** causa uma viagem de ida e volta ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações em uma única linha, será mais eficiente enviar todas as alterações com uma única chamada de **SetData**.  
  
 No modo de atualização atrasada, uma viagem de ida e volta é feita ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada linha indicada nos parâmetros *cRows* e *rghRows* de **IRowsetUpdate::Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Quando você estiver usando **IRowsetUpdate:: Update**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo tentará processar cada linha indicada. Um erro ocorrido devido a dados inválidos, comprimento ou valores de status para qualquer linha não interrompe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o processamento do provedor de OLE DB nativo do cliente. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor deve examinar a matriz *prgRowstatus* retornada para determinar a falha de qualquer linha específica quando [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] o provedor de OLE DB de cliente nativo retornar DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte Também  
 [Atualizando dados em conjuntos de linhas](updating-data-in-rowsets.md)  
  
  
