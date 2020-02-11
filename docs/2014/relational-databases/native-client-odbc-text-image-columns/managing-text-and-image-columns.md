---
title: Gerenciando colunas de texto e imagem | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
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
manager: craigg
ms.openlocfilehash: a161b009239db3c17acb64f8d8eeaaa61321cd9f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63195321"
---
# <a name="managing-text-and-image-columns"></a>Gerenciando colunas de texto e imagem
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]os dados **Text**, **ntext**e **Image** (também conhecidos como Long Data) são tipos de dados character ou Binary String que podem conter valores de dados muito grandes para se ajustarem às colunas **Char**, **varchar**, **Binary**ou **varbinary** . O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipo de dados **Text** é mapeado para o tipo de dados ODBC SQL_LONGVARCHAR; **ntext** mapeia para SQL_WLONGVARCHAR; e mapas de **imagem** para SQL_LONGVARBINARY. Alguns itens de dados, como documentos longos ou bitmaps grandes, podem ser muito grandes para serem armazenados na memória de forma aceitável. Para recuperar dados longos de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] partes sequenciais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC do Native Client permite que um aplicativo chame [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Para enviar dados longos em partes sequenciais, o aplicativo pode chamar [SQLPutData](../native-client-odbc-api/sqlputdata.md). Os parâmetros para os quais os dados são enviados no tempo de execução são conhecidos como parâmetros de dados em execução.  
  
 Um aplicativo pode realmente gravar ou recuperar qualquer tipo de dados (não apenas dados longos) com **SQLPutData** ou **SQLGetData**, embora apenas dados de **caracteres** e **binários** possam ser enviados ou recuperados em partes. No entanto, se os dados forem pequenos o suficiente para caber em um único buffer, geralmente não há motivo para usar **SQLPutData** ou **SQLGetData**. É muito mais fácil associar o único buffer ao parâmetro ou à coluna.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Colunas image e text associadas e não associadas](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificações não registradas e registradas](logged-vs-unlogged-modifications.md)  
  
-   [Dados em execução e colunas Text, ntext ou Image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
