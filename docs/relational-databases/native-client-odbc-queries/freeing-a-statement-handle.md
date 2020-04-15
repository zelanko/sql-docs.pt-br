---
title: Liberando uma alça de declaração | Microsoft Docs
ms.custom: ''
ms.date: 03/03/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- reusing statement handles
- freeing statement handles
- statements [ODBC], statement handles
- SQLFreeStmt function
- ODBC applications, statements
- statement handles [ODBC]
ms.assetid: 96fdff84-0ca7-460a-a240-94ee826ea41c
author: markingmyname
ms.author: maghan
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 7e954773f85afc434d1e5bd18f7ffb76e28a1438
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81297883"
---
# <a name="freeing-a-statement-handle"></a>Liberando um identificador de instrução
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  É mais eficiente reutilizar identificadores de instrução do que eliminá-los e alocar novos. Antes de executar uma nova instrução SQL em um identificador de instrução, os aplicativos deverão verificar se as configurações de instrução atuais são apropriadas. Essas configurações incluem atributos de instrução, associações de parâmetro e associações de conjunto de resultados. Geralmente, parâmetros e conjuntos de resultados para a antiga declaração SQL devem ser desvinculados ligando para [sqlfreestmt](../../relational-databases/native-client-odbc-api/sqlfreestmt.md) com as opções SQL_RESET_PARAMS e SQL_UNBIND e, em seguida, revinculado para a nova declaração SQL.  
  
 Quando o aplicativo terminar de usar a declaração, ele chama [sqlfreehandle](../../relational-databases/native-client-odbc-api/sqlfreehandle.md) para liberar a declaração. Observe que **o SQLDisconnect** libera automaticamente todas as instruções em uma conexão.  
  
## <a name="see-also"></a>Consulte Também  
 [Execução de consultas &#40;&#41;ODBC](../../relational-databases/native-client-odbc-queries/executing-queries-odbc.md)  
  
  
