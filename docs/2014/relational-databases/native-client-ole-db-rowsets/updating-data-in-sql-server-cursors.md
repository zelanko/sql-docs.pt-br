---
title: Atualizando dados em cursores do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- isolation levels [SQL Server]
- delayed update mode [OLE DB]
- immediate update mode [OLE DB]
- cursors [OLE DB]
- data updates [SQL Server], OLE DB
ms.assetid: 732dafee-f2d5-4aef-aad7-3a8bf3b1e876
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: caa3f5d35d51a90809175da88c9732fd883d291d
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37428325"
---
# <a name="updating-data-in-sql-server-cursors"></a>Atualizando dados em cursores do SQL Server
  Ao buscar e atualizar dados por meio [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores, um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aplicativo de consumidor do provedor OLE DB do Native Client está ligado pelas mesmas considerações e restrições que se aplicam a qualquer outro aplicativo cliente.  
  
 Apenas as linhas em cursores do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] participam do controle de acesso a dados simultâneo. Quando o consumidor solicita um conjunto de linhas modificável, o controle de simultaneidade é controlado por DBPROP_LOCKMODE. Para modificar o nível do controle de acesso simultâneo, o consumidor define a propriedade DBPROP_LOCKMODE antes de abrir o conjunto de linhas.  
  
 Os níveis de isolamento da transação podem gerar defasagens significativas no posicionamento de linhas, se o design do aplicativo cliente permitir que as transações permaneçam abertas por longos períodos. Por padrão, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client usa o nível de isolamento de leitura confirmada especificado por DBPROPVAL_TI_READCOMMITTED. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte ao isolamento de leitura suja quando a simultaneidade do conjunto de linhas é somente leitura. Assim, o consumidor pode solicitar um nível mais alto de isolamento em um conjunto de linhas modificável, mas não pode solicitar nenhum nível inferior com êxito.  
  
## <a name="immediate-and-delayed-update-modes"></a>Modos de atualização imediatos e atrasados  
 No modo de atualização imediata, cada chamada para **IRowsetChange:: SetData** causa uma viagem para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Se o consumidor fizer várias alterações a uma única linha, é mais eficiente enviar todas as alterações com uma única **SetData** chamar.  
  
 No modo de atualização com atraso, uma ida e volta é feita para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para cada linha indicada na *cRows* e *rghRows* parâmetros da **IRowsetUpdate:: Update**.  
  
 Em qualquer modo, uma viagem de ida e volta representará uma transação distinta quando nenhum objeto de transação estiver aberto para o conjunto de linhas.  
  
 Quando você estiver usando **IRowsetUpdate:: Update**, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB do Native Client tenta processar cada linha indicada. Um erro que ocorre devido a valores de dados, comprimento ou status inválidos para qualquer linha não interrompe [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] processamento do provedor OLE DB do Native Client. É possível modificar todas ou nenhuma das outras linhas que participam da atualização. O consumidor deve examinar a *prgRowStatus* matriz para determinar a falha para qualquer determinado de linhas quando o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client retorna DB_S_ERRORSOCCURRED.  
  
 Um consumidor não deve presumir que as linhas são processadas em qualquer ordem específica. Se um consumidor solicitar o processamento ordenado da modificação de dados em mais de uma única linha, ele deverá estabelecer essa ordem na lógica do aplicativo e abrir uma transação para conter o processo.  
  
## <a name="see-also"></a>Consulte também  
 [Atualizando dados em conjuntos de linhas](updating-data-in-rowsets.md)  
  
  
