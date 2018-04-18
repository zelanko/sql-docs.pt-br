---
title: Gerenciar colunas de texto e imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: ''
ms.component: native-client-odbc-text-image-columns
ms.reviewer: ''
ms.suite: sql
ms.technology: ''
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
caps.latest.revision: 31
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
monikerRange: '>= aps-pdw-2016 || = azuresqldb-current || = azure-sqldw-latest || >= sql-server-2016 || = sqlallproducts-allversions'
ms.openlocfilehash: 95252e6bebed7c791fc50fef9e7f0ece65231198
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="managing-text-and-image-columns"></a>Gerenciando colunas de texto e imagem
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto**, **ntext**, e **imagem** dados (também conhecidos como dados longos) são caracteres ou tipos de dados de cadeia de caracteres binária que podem conter valores de dados muito grandes para caber na **char**, **varchar**, **binário**, ou **varbinary** colunas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto** mapeia para o tipo de dados ODBC SQL_LONGVARCHAR; tipo de dados **ntext** mapeado para SQL_WLONGVARCHAR e **imagem** mapeado para SQL_LONGVARBINARY. Alguns itens de dados, como documentos longos ou bitmaps grandes, podem ser muito grandes para serem armazenados na memória de forma aceitável. Para recuperar dados longos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em partes sequenciais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client permite que um aplicativo chamar [SQLGetData](../../relational-databases/native-client-odbc-api/sqlgetdata.md). Para enviar dados longos em partes sequenciais, o aplicativo pode chamar [SQLPutData](../../relational-databases/native-client-odbc-api/sqlputdata.md). Os parâmetros para os quais os dados são enviados no tempo de execução são conhecidos como parâmetros de dados em execução.  
  
 Um aplicativo pode realmente gravar ou recuperar qualquer tipo de dados (não apenas longos) com **SQLPutData** ou **SQLGetData**, embora somente **caracteres** e  **binário** dados podem ser enviados ou recuperados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData** ou **SQLGetData**. É muito mais fácil associar o único buffer ao parâmetro ou à coluna.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Colunas Text e Image associadas vs. não associadas](../../relational-databases/native-client-odbc-text-image-columns/bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificações registradas vs. não registradas](../../relational-databases/native-client-odbc-text-image-columns/logged-vs-unlogged-modifications.md)  
  
-   [Dados em execução e colunas Text, ntext ou Image](../../relational-databases/native-client-odbc-text-image-columns/data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte também  
 [Cliente nativo do SQL Server & #40; ODBC & #41;](../../relational-databases/native-client/odbc/sql-server-native-client-odbc.md)  
  
  
