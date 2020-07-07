---
title: Dados em execução e Text, ntext, Image
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], image
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- ODBC data types, text columns
- data-at-execution
- ODBC data-at-execution
- image columns [ODBC]
ms.assetid: 67ffb1a6-f38d-4712-ba64-96bdd41ec2b2
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 189058d9e15b0dfd9fa59108c2a8ba173765ac23
ms.sourcegitcommit: f3321ed29d6d8725ba6378d207277a57cb5fe8c2
ms.contentlocale: pt-BR
ms.lasthandoff: 07/06/2020
ms.locfileid: "86004287"
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Dados em execução e colunas Text, ntext ou Image
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

  Os dados em execução ODBC são um recurso que permite aos aplicativos trabalhar com quantidades extremamente grandes de dados em parâmetros ou colunas associadas. Ao recuperar colunas de **texto**, **ntext**ou **Image** muito grandes, um aplicativo pode não ser capaz de simplesmente alocar um buffer enorme, associar a coluna ao buffer e buscar a linha. Ao atualizar colunas de **texto**, **ntext**ou **Image** muito grandes, o aplicativo pode não ser capaz de simplesmente alocar um buffer enorme, associá-lo a um marcador de parâmetro em uma instrução SQL e, em seguida, executar a instrução. Nesses casos, o aplicativo deve usar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) ou [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) com suas opções de dados em execução.  
  
## <a name="see-also"></a>Consulte Também  
 [Gerenciando colunas de texto e imagem](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
