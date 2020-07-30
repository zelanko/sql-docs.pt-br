---
title: Tipos de dados (provedor de OLE DB de cliente nativo) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- mapping data types [OLE DB]
- SQL Server Native Client OLE DB provider, data types
- data types [OLE DB]
- OLE DB, data types
ms.assetid: 15953706-f0d1-45f5-a2eb-a8bd36e1a5fc
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: e1574b87bef2e231415b0c95a333c4b7107ca726
ms.sourcegitcommit: 216f377451e53874718ae1645a2611cdb198808a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87245878"
---
# <a name="sql-server-native-client-data-types-ole-db"></a>Tipos de dados de SQL Server Native Client (OLE DB)
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Para executar [!INCLUDE[tsql](../../includes/tsql-md.md)] instruções e processar os resultados usando o provedor de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] OLE DB de cliente nativo, você deve saber como o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] provedor de OLE DB de cliente nativo mapeia [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados para OLE DB tipos de dados ao associar parâmetros ou colunas em um conjunto de linhas e quando ele usa a interface **ITableDefinition** para criar uma tabela no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Mapeamento de tipos de dados em conjuntos de linhas e parâmetros](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-rowsets-and-parameters.md)  
  
-   [Mapeamento do tipo de dados em ITableDefinition](../../relational-databases/native-client-ole-db-data-types/data-type-mapping-in-itabledefinition.md)  
  
-   [Estrutura SSVARIANT](../../relational-databases/native-client-ole-db-data-types/ssvariant-structure.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;OLE DB&#41;](../../relational-databases/native-client/ole-db/sql-server-native-client-ole-db.md)  
  
  
