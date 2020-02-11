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
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 19efcc8b4381694177d0ec3d64376368e8d23a7d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73779772"
---
# <a name="batches-of-statements"></a>Lotes de instruções
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  Um lote de [!INCLUDE[tsql](../../../includes/tsql-md.md)] instruções contém duas ou mais instruções, separadas por um ponto-e-vírgula (;), criado em uma única cadeia de caracteres passada para a função **SQLExecDirect** ou [SQLPrepare](https://go.microsoft.com/fwlink/?LinkId=59360). Por exemplo:  
  
```  
SQLExecDirect(hstmt,   
    "SELECT * FROM Authors; SELECT * FROM Titles",  
    SQL_NTS);  
```  
  
 Os lotes podem ser mais eficientes do que enviar instruções separadamente porque o tráfego de rede costuma ser reduzido. Use [SQLMoreResults](../../../relational-databases/native-client-odbc-api/sqlmoreresults.md) para ficar posicionado no próximo conjunto de resultados quando terminar com o conjunto de resultados atual.  
  
 Os lotes sempre podem ser usados quando os atributos de cursor ODBC são definidos como os padrões de um cursor de somente encaminhamento, somente leitura, com um tamanho do conjunto de linhas igual a 1.  
  
 Caso um lote seja executado durante o uso de cursores de servidor no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)], o cursor de servidor é convertido implicitamente em um conjunto de resultados padrão. **SQLExecDirect** ou **SQLExecute** retornam SQL_SUCCESS_WITH_INFO e uma chamada para **SQLGetDiagRec** retorna:  
  
```  
szSqlState = "01S02", pfNativeError = 0  
szErrorMsg = "[Microsoft][SQL Server Native Server Native Client]Cursor type changed."  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Executando instruções &#40;&#41;ODBC](../../../relational-databases/native-client-odbc-queries/executing-statements/executing-statements-odbc.md)  
  
  
