---
title: "Buscando uma única linha com IRow | Microsoft Docs"
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
- fetching rows
- IRow interface
- single row fetching [SQL Server Native Client]
- OLE DB rowsets, fetching
- rowsets [OLE DB], fetching
- SQL Server Native Client OLE DB provider, fetching
ms.assetid: 07c803ca-299a-42c5-ba02-360b9631d15f
caps.latest.revision: "31"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: efefde48815f09ccc6a99dc97a311ad82aa3ba63
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="fetching-a-single-row-with-irow"></a>Buscando uma única linha com IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O **IRow** implementação da interface de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor do OLE DB Native Client é simplificado para aumentar o desempenho. **IRow** permite acesso direto a colunas de um objeto de única linha. Se você souber com antecedência que o resultado de uma execução de comando produzirá exatamente uma linha, **IRow** recuperará as colunas dessa linha. Se o conjunto de resultados inclui várias linhas, **IRow** irá expor apenas a primeira linha.  
  
 O **IRow** implementação não permite nenhuma navegação da linha. Todas as colunas na linha são acessadas apenas uma vez com uma exceção: uma coluna pode ser acessada uma vez para localizar o tamanho da coluna e novamente para buscar os dados.  
  
> [!NOTE]  
>  **IRow:: Open** dá suporte ao tipo DBGUID_STREAM e DBGUID_NULL somente de objetos a ser aberto.  
  
 Para obter um objeto de linha usando **ICommand:: execute** método, IID_IRow deve ser passado. O **IMultipleResults** interface deve ser usada para manipular vários conjuntos de resultados. **IMultipleResults** dá suporte a **IRow** e **IRowset**. **IRowset** é usada para operações em massa.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IRow::GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [Buscando dados BLOB usando IRow](http://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>Consulte Também  
 [Conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
