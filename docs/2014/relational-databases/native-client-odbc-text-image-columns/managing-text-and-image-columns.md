---
title: Gerenciando colunas Text e Image | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
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
caps.latest.revision: 30
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f0989157eabe987ae8d1bdac22deb25ad2c6d028
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37426985"
---
# <a name="managing-text-and-image-columns"></a>Gerenciando colunas de texto e imagem
  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto**, **ntext**, e **imagem** dados (também conhecidos como dados longos) são o caractere ou tipos de dados de cadeia de caracteres binária que podem conter valores de dados muito grandes para caber na **char**, **varchar**, **binário**, ou **varbinary** colunas. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] **texto** mapeia para o tipo de dados ODBC SQL_LONGVARCHAR; tipo de dados **ntext** é mapeado para SQL_WLONGVARCHAR e **imagem** é mapeado para SQL_LONGVARBINARY. Alguns itens de dados, como documentos longos ou bitmaps grandes, podem ser muito grandes para serem armazenados na memória de forma aceitável. Para recuperar dados longos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em partes sequenciais, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] driver ODBC Native Client permite que um aplicativo chamar [SQLGetData](../native-client-odbc-api/sqlgetdata.md). Para enviar dados longos em partes sequenciais, o aplicativo pode chamar [SQLPutData](../native-client-odbc-api/sqlputdata.md). Os parâmetros para os quais os dados são enviados no tempo de execução são conhecidos como parâmetros de dados em execução.  
  
 Um aplicativo pode realmente gravar ou recuperar qualquer tipo de dados (dados não apenas longos) com **SQLPutData** ou **SQLGetData**, embora somente **caractere** e  **binário** dados podem ser enviados ou recuperados em partes. No entanto, se os dados são pequenos o suficiente para caber em um único buffer, há geralmente não há motivo para usar **SQLPutData** ou **SQLGetData**. É muito mais fácil associar o único buffer ao parâmetro ou à coluna.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Colunas Text e Image associadas vs. não associadas](bound-vs-unbound-text-and-image-columns.md)  
  
-   [Modificações registradas vs. não registradas](logged-vs-unlogged-modifications.md)  
  
-   [Dados em execução e colunas Text, ntext ou Image](data-at-execution-and-text-ntext-or-image-columns.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)  
  
  
