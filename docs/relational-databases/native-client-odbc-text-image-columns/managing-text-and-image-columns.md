---
title: Gerenciando colunas Text e Image | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.reviewer: ''
ms.suite: sql
ms.technology: native-client
ms.tgt_pltfrm: ''
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
manager: craigg
monikerRange: '>=aps-pdw-2016||=azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current'
ms.openlocfilehash: 5b086c321e78c626eaa171ec1ee68f6c690c4362
ms.sourcegitcommit: 4183dc18999ad243c40c907ce736f0b7b7f98235
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/27/2018
ms.locfileid: "43078188"
---
# <a name="managing-text-and-image-columns"></a>Gerenciando colunas de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto**, **ntext**, e **imagem** dados (também conhecidos como dados longos) são o caractere ou tipos de dados de cadeia de caracteres binária que podem conter valores de dados muito grandes para caber na **char**, **varchar**, **binário**, ou **varbinary** colunas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto** mapeia para o tipo de dados ODBC SQL_LONGVARCHAR; tipo de dados **ntext** é mapeado para SQL_WLONGVARCHAR e **imagem** é mapeado para SQL_LONGVARBINARY. Alguns itens de dados, como documentos longos ou bitmaps grandes, podem ser muito grandes para serem armazenados na memória de forma aceitável. Para recuperar dados longos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em partes sequenciais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client permite que um aplicativo chamar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Para enviar dados longos em partes sequenciais, o aplicativo pode chamar [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Os parâmetros para os quais os dados são enviados no tempo de execução são conhecidos como parâmetros de dados em execução.  
  
 Um aplicativo pode realmente gravar ou recuperar qualquer tipo de dados (dados não apenas longos) com **SQLPutData** ou **SQLGetData**, embora somente **caractere** e  **binário** dados podem ser enviados ou recuperados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData** ou **SQLGetData**. É muito mais fácil associar o único buffer ao parâmetro ou à coluna.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Colunas Text e Image associadas vs. não associadas](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificações registradas vs. não registradas](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Dados em execução e colunas Text, ntext ou Image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
