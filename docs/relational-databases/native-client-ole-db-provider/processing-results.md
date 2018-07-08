---
title: Processando resultados | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.component: native-client-ole-db-provider
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client OLE DB provider, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [SQL Server Native Client]
ms.assetid: 20887ac4-f649-4e7f-92e6-f929e2e70952
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 3c8b6a1653fa089b5ef78211c4dd1ab4896dbcf6
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37425895"
---
# <a name="processing-results"></a>Processando resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Caso um objeto de conjunto de linhas seja produzido pela execução de um comando ou pela geração direta de um objeto de conjunto de linhas no provedor, o consumidor precisa recuperar e acessar dados no conjunto de linhas.  
  
 Conjuntos de linhas são os objetos centrais que permitem ao provedor OLE DB do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client expor dados em forma tabular. Conceitualmente, um conjunto de linhas é um conjunto de linhas em que cada linha tem dados de coluna. Um objeto de conjunto de linhas expõe interfaces como **IRowset** (contém métodos para buscar linhas do conjunto de linhas em sequência), **IAccessor** (permite a definição de um grupo de associações de coluna que descreve o dados tabulares de forma são associados a variáveis de programa do consumidor), **IColumnsInfo** (fornece informações sobre colunas no conjunto de linhas), e **IRowsetInfo** (fornece informações sobre o conjunto de linhas).  
  
 Um consumidor pode chamar o **IRowset:: GetData** método para recuperar uma linha de dados do conjunto de linhas em um buffer. Antes de **GetData** é chamado, o consumidor descreve o buffer usando um conjunto de estruturas DBBINDING. Cada associação descreve como uma coluna em um conjunto de linhas é armazenada em um buffer de consumidor e contém o seguinte:  
  
-   Ordinal da coluna (ou parâmetro) a que a associação se aplica.  
  
-   Informações sobre a associação (por exemplo, valor de dados, comprimento dos dados e o status da associação).  
  
-   Informações sobre o que é deslocado no buffer para cada uma das partes.  
  
-   Comprimento e tipo dos valores de dados como se apresentam no buffer de consumidor.  
  
 Ao obter os dados, o provedor usa informações de cada associação para determinar onde e como recuperar dados do buffer de consumidor. Ao definir dados no buffer de consumidor, o provedor usa informações de cada associação para determinar onde e como retornar dados no buffer.  
  
 Depois que as estruturas DBBINDING são especificadas, um acessador é criado (**IAccessor:: CreateAccessor**). Um acessador é uma coleção de associações, sendo usado para obter ou definir os dados no buffer de consumidor.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo de provedor do SQL Server Native Client OLE DB](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)   
 [Tópicos de instruções do OLE DB](../../relational-databases/native-client-ole-db-how-to/ole-db-how-to-topics.md)  
  
  
