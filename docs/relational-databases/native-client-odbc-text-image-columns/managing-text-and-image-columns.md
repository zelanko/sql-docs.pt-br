---
title: Gerenciando colunas de texto e imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- text columns [ODBC]
- SQL Server Native Client ODBC driver, image columns
- SQL Server Native Client ODBC driver, text columns
- data types [ODBC], text
- columns [ODBC]
- ODBC data types, image columns
- data types [ODBC], mapping
- ODBC data types, text columns
- image columns [ODBC]
ms.assetid: 7b543556-ff36-4d35-ac08-de96223d92cd
author: MightyPen
ms.author: genemi
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 221d83188a3d48fe5383a109b878c7b5a59bdad5
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "73758399"
---
# <a name="managing-text-and-image-columns"></a>Gerenciando colunas de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os dados **Text**, **ntext**e **Image** (também conhecidos como Long Data) são tipos de dados character ou Binary String que podem conter valores de dados muito grandes para se ajustarem às colunas **Char**, **varchar**, **Binary**ou **varbinary** . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados **Text** é mapeado para o tipo de dados ODBC SQL_LONGVARCHAR; **ntext** mapeia para SQL_WLONGVARCHAR; e mapas de **imagem** para SQL_LONGVARBINARY. Alguns itens de dados, como documentos longos ou bitmaps grandes, podem ser muito grandes para serem armazenados na memória de forma aceitável. Para recuperar dados longos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] partes sequenciais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client permite que um aplicativo chame [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Para enviar dados longos em partes sequenciais, o aplicativo pode chamar [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Os parâmetros para os quais os dados são enviados no tempo de execução são conhecidos como parâmetros de dados em execução.  
  
 Um aplicativo pode realmente gravar ou recuperar qualquer tipo de dados (não apenas dados longos) com **SQLPutData** ou **SQLGetData**, embora apenas dados de **caracteres** e **binários** possam ser enviados ou recuperados em partes. No entanto, se os dados forem pequenos o suficiente para caber em um único buffer, geralmente não há motivo para usar **SQLPutData** ou **SQLGetData**. É muito mais fácil associar o único buffer ao parâmetro ou à coluna.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Colunas image e text associadas e não associadas](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificações não registradas e registradas](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Dados em execução e colunas Text, ntext ou Image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
