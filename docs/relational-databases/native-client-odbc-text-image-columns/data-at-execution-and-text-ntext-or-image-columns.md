---
title: "Dados em execução e Text, ntext ou colunas de imagem | Microsoft Docs"
ms.custom: 
ms.date: 03/06/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-text-image-columns
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
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
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ec54f186ac60d970d5e3848d5abafd4d6cd636c5
ms.sourcegitcommit: 9e6a029456f4a8daddb396bc45d7874a43a47b45
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/25/2018
---
# <a name="data-at-execution-and-text-ntext-or-image-columns"></a>Dados em execução e colunas Text, ntext ou Image
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  Os dados em execução ODBC são um recurso que permite aos aplicativos trabalhar com quantidades extremamente grandes de dados em parâmetros ou colunas associadas. Ao recuperar grandes **texto**, **ntext**, ou **imagem** colunas, um aplicativo não consiga simplesmente alocar um buffer enorme, associar a coluna no buffer e buscar a linha. Ao atualizar muito grandes **texto**, **ntext**, ou **imagem** colunas, o aplicativo não consiga simplesmente alocar um buffer enorme, associá-lo a um marcador de parâmetro em um SQL instrução e, em seguida, execute a instrução. Nesses casos, o aplicativo deve usar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md) ou [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md) com suas opções de dados em execução.  
  
## <a name="see-also"></a>Consulte também  
 [Gerenciando colunas Text e Image](../../relational-databases/native-client-odbc-text-image-columns/managing-text-and-image-columns.md)  
  
  
