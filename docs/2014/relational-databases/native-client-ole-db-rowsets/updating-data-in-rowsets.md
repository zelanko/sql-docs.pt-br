---
title: Atualizando dados em conjuntos de linhas | Microsoft Docs
ms.custom: ''
ms.date: 04/27/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- updating data [SQL Server]
- rowsets [OLE DB], updating data
- SQL Server Native Client OLE DB provider, rowsets
- OLE DB rowsets, updating data
- SQL Server Native Client OLE DB provider, data updates
- data updates [SQL Server], OLE DB
ms.assetid: 37769b1c-c480-419a-8c54-5cc420bf73db
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f68e4f2be641d6c6aeaf8bbbfcc8cad81ab1a39a
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48130969"
---
# <a name="updating-data-in-rowsets"></a>Atualizando dados em conjuntos de linhas
  O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] as atualizações do provedor OLE DB do Native Client [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] dados quando um consumidor atualiza um conjunto de linhas modificável que contém os dados. Um conjunto de linhas modificável é criado quando o consumidor solicita suporte para a interface **IRowsetChange** ou **IRowsetUpdate**.  
  
 Todos os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] conjuntos de linhas modificáveis do provedor OLE DB do Native Client usam [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] cursores para dar suporte ao conjunto de linhas. A propriedade do conjunto de linhas DBPROP_LOCKMODE altera o comportamento de controle da simultaneidade do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em cursores e determina o comportamento da busca de linhas do conjunto de linhas e da geração de erros de integridade de dados nos conjuntos de linhas atualizáveis.  
  
 O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client dá suporte à sincronização de linha antes ou após uma atualização.  
  
> [!NOTE]  
>  IRowChange::SetColumns está disponível para definir os valores de uma ou mais colunas nomeadas de um objeto de linha.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Atualizando dados em cursores do SQL Server](updating-data-in-sql-server-cursors.md)  
  
-   [Ressincronizando linhas](updating-data-in-rowsets-resynchronizing-rows.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](rowsets.md)  
  
  
