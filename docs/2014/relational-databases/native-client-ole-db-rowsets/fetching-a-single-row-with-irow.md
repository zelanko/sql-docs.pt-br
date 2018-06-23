---
title: Buscando uma única linha com IRow | Microsoft Docs
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
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
caps.latest.revision: 30
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: eef27a6cbd6ee793cd227c2cf6e6570e1d04b004
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117880"
---
# <a name="fetching-a-single-row-with-irow"></a>Buscando uma única linha com IRow
  O **IRow** implementação da interface de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client é simplificado para aumentar o desempenho. **IRow** permite acesso direto a colunas de um objeto de única linha. Se você souber com antecedência que o resultado de uma execução de comando produzirá exatamente uma linha, **IRow** recuperará as colunas dessa linha. Se o conjunto de resultados inclui várias linhas, **IRow** irá expor apenas a primeira linha.  
  
 O **IRow** implementação não permite nenhuma navegação da linha. Todas as colunas na linha são acessadas apenas uma vez com uma exceção: uma coluna pode ser acessada uma vez para localizar o tamanho da coluna e novamente para buscar os dados.  
  
> [!NOTE]  
>  **IRow:: Open** dá suporte ao tipo DBGUID_STREAM e DBGUID_NULL somente de objetos a ser aberto.  
  
 Para obter um objeto de linha usando **ICommand:: execute** método, IID_IRow deve ser passado. O **IMultipleResults** interface deve ser usada para manipular vários conjuntos de resultados. **IMultipleResults** dá suporte a **IRow** e **IRowset**. **IRowset** é usada para operações em massa.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IRow::GetColumns](using-irow-getcolumns.md)  
  
-   [Buscando dados BLOB usando IRow](../../database-engine/dev-guide/fetching-blob-data-using-irow.md)  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](rowsets.md)  
  
  