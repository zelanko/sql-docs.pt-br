---
title: 'Usando IRow:: Getcolumns | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- GetColumns method
ms.assetid: 1f5d2e03-e6fe-4ea1-b71d-55d02b5d59ae
caps.latest.revision: 29
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 37c7895a888852a8acb0b73a4b44e297e1ea3318
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36020910"
---
# <a name="using-irowgetcolumns"></a>Usando IRow::GetColumns
  O **IRow** implementação permite acesso sequencial somente de encaminhamento para as colunas. Você pode acessar todas as colunas na linha com uma única chamada para **IRow:: Getcolumns** ou chame **IRow:: Getcolumns** várias vezes sempre que você acessa várias colunas na linha.  
  
 As várias chamadas para **IRow:: Getcolumns** não devem se sobrepor. Por exemplo, se a primeira chamada para **IRow:: Getcolumns** recupera colunas 1, 2 e 3, a segunda chamada para **IRow:: Getcolumns** deve chamar as colunas 4, 5 e 6. Se chamadas posteriores para **IRow:: Getcolumns** se sobrepõem, o sinalizador de status (campo dwstatus em DBCOLUMNACCESS) é definido como DBSTATUS_E_UNAVAILABLE.  
  
## <a name="see-also"></a>Consulte também  
 [Buscando uma única linha com IRow](fetching-a-single-row-with-irow.md)  
  
  