---
title: Usando a cláusula OUTPUT com OLE DB no SQL Server Native Client | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
ms.assetid: 53deeb99-c088-4fde-844b-b2d91d6de1eb
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: c664a77ea3087e7fd94898e51d374519c0c29e01
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68035532"
---
# <a name="using-the-output-clause-with-ole-db-in-sql-server-native-client"></a>Usando a cláusula OUTPUT com OLE DB no SQL Server Native Client
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Se você usar uma cláusula OUTPUT em um comando INSERT, UPDATE, DELETE ou MERGE, a contagem de linhas afetadas não estará disponível. O aplicativo deve contar o número de linhas no conjunto de linhas retornado pela cláusula OUTPUT.  
  
## <a name="see-also"></a>Consulte também  
 [Criando um aplicativo provedor OLE DB do SQL Server Native Client](../../relational-databases/native-client-ole-db-provider/creating-a-sql-server-native-client-ole-db-provider-application.md)  
  
  
