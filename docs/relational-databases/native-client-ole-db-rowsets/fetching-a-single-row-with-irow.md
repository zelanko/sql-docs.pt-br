---
title: Buscando uma única linha com IRow | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: dd5083da174c37d1e7fabae40bac5f97ac7f88d3
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43082519"
---
# <a name="fetching-a-single-row-with-irow"></a>Buscando uma única linha com IRow
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  O **IRow** implementação da interface de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor OLE DB do Native Client é simplificada para aumentar o desempenho. **IRow** permite o acesso direto a colunas de um único objeto de linha. Se você souber com antecedência que o resultado de uma execução de comando produzirá exatamente uma linha, **IRow** recuperará as colunas da linha. Se o conjunto de resultados incluir várias linhas, **IRow** exporá apenas a primeira linha.  
  
 A implementação de **IRow** não permite nenhuma navegação da linha. Todas as colunas na linha são acessadas apenas uma vez com uma exceção: uma coluna pode ser acessada uma vez para localizar o tamanho da coluna e novamente para buscar os dados.  
  
> [!NOTE]  
>  **IRow::Open** só dá suporte à abertura do tipo de objetos DBGUID_STREAM e DBGUID_NULL.  
  
 Para obter um objeto de linha que usa o método **ICommand::Execute**, IID_IRow precisa ser passado. A interface **IMultipleResults** precisa ser usada para manipular vários conjuntos de resultados. **IMultipleResults** dá suporte a **IRow** e **IRowset**. **IRowset** é usado para operações em massa.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Usando IRow::GetColumns](../../relational-databases/native-client-ole-db-rowsets/using-irow-getcolumns.md)  
  
-   [Buscando dados BLOB usando IRow](http://msdn.microsoft.com/library/badbd6ac-20aa-4891-a14f-48d38e7f30de)  
  
## <a name="see-also"></a>Consulte também  
 [Conjuntos de linhas](../../relational-databases/native-client-ole-db-rowsets/rowsets.md)  
  
  
