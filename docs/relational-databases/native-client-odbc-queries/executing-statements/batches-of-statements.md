---
title: Lotes de instruções | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- statements [ODBC], batches
- batches [ODBC]
- ODBC applications, statements
- multiple statements, batches
- SQLMoreResults function
- SQLExecDirect function
ms.assetid: 057d7c1c-1428-4780-9447-a002ea741188
author: MightyPen
ms.author: genemi
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 651ff25ac3331820f93fae7cdd5fc85567738107
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47851964"
---
# <a name="batches-of-statements"></a>Lotes de instruções
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../../includes/snac-deprecated.md)]

  Um lote de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções contém duas ou mais instruções, separadas por ponto e vírgula (;), criado em uma única cadeia de caracteres passada para **SQLExecDirect** ou [função SQLPrepare](http://go.microsoft.com/fwlink/?LinkId=59360). Por exemplo:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 Os lotes podem ser mais eficientes do que enviar instruções separadamente porque o tráfego de rede costuma ser reduzido. Use [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para se posicionar quanto o próximo conjunto de resultados quando concluído com o conjunto de resultados atual.  
  
 Os lotes sempre podem ser usados quando os atributos de cursor ODBC são definidos como os padrões de um cursor de somente encaminhamento, somente leitura, com um tamanho do conjunto de linhas igual a 1.  
  
 Caso um lote seja executado durante o uso de cursores de servidor no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o cursor de servidor é convertido implicitamente em um conjunto de resultados padrão. **SQLExecDirect** ou **SQLExecute** retornar SQL_SUCCESS_WITH_INFO e uma chamada **SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Consulte também  
 [Executar instruções &#40;ODBC&#41;](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
