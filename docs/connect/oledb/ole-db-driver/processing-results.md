---
title: Processando resultados | Microsoft Docs
description: Processando resultados
ms.custom: ''
ms.date: 03/26/2018
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: oledb-driver-for-sql-server
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- OLE DB Driver for SQL Server, results processing
- OLE DB, processing results
- rowsets [SQL Server], results processing
- results [OLE DB Driver for SQL Server]
author: pmasl
ms.author: Pedro.Lopes
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6b564e696b28ca751179376f66458f7b11652ad9
ms.sourcegitcommit: 9351e8b7b68f599a95fb8e76930ab886db737e5f
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/06/2018
---
# <a name="processing-results"></a>Processando resultados
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Caso um objeto de conjunto de linhas seja produzido pela execução de um comando ou pela geração direta de um objeto de conjunto de linhas no provedor, o consumidor precisa recuperar e acessar dados no conjunto de linhas.  
  
 Conjuntos de linhas são os objetos centrais que permitem que o Driver OLE DB para SQL Server para expor dados em formato tabular. Conceitualmente, um conjunto de linhas é um conjunto de linhas em que cada linha tem dados de coluna. Um objeto de conjunto de linhas expõe interfaces como **IRowset** (contém métodos para buscar linhas do conjunto de linhas em sequência), **IAccessor** (permite a definição de um grupo de associações de coluna que descreve a maneira como os dados de tabela são associados a variáveis de programa do consumidor), **IColumnsInfo** (fornece informações sobre colunas no conjunto de linhas), e **IRowsetInfo** (fornece informações sobre o conjunto de linhas).  
  
 Um consumidor pode chamar o **IRowset:: GetData** método para recuperar uma linha de dados do conjunto de linhas em um buffer. Antes de **GetData** é chamado, o consumidor descreve o buffer usando um conjunto de estruturas DBBINDING. Cada associação descreve como uma coluna em um conjunto de linhas é armazenada em um buffer de consumidor e contém o seguinte:  
  
-   Ordinal da coluna (ou parâmetro) a que a associação se aplica.  
  
-   Informações sobre a associação (por exemplo, valor de dados, comprimento dos dados e o status da associação).  
  
-   Informações sobre o que é deslocado no buffer para cada uma das partes.  
  
-   Comprimento e tipo dos valores de dados como se apresentam no buffer de consumidor.  
  
 Ao obter os dados, o provedor usa informações de cada associação para determinar onde e como recuperar dados do buffer de consumidor. Ao definir dados no buffer de consumidor, o provedor usa informações de cada associação para determinar onde e como retornar dados no buffer.  
  
 Depois que as estruturas DBBINDING são especificadas, um acessador é criado (**IAccessor:: CreateAccessor**). Um acessador é uma coleção de associações, sendo usado para obter ou definir os dados no buffer de consumidor.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um Driver do OLE DB para o aplicativo do SQL Server](../../oledb/ole-db-driver/creating-a-oledb-driver-for-sql-server-application.md)   
 [Tópicos de instruções do OLE DB](../../oledb/ole-db-how-to/ole-db-how-to-topics.md)  
  
  
