---
title: Comunicando-se com o SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: native-client
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
caps.latest.revision: 33
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a701075067b89e40d8dfe44bf9dccfb3240960f1
ms.sourcegitcommit: f8ce92a2f935616339965d140e00298b1f8355d7
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/03/2018
ms.locfileid: "37414375"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicando-se com o SQL Server (ODBC)
  Para um aplicativo ODBC se comunique com uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], ele deve alocar o ambiente e trata de conexão e conecte-se à fonte de dados. Depois que uma conexão é estabelecida, o aplicativo pode enviar consultas ao servidor e processar quaisquer conjuntos de resultados. Quando o aplicativo conclui o uso da fonte de dados, ele se desconecta da fonte de dados e libera o identificador de conexão. Depois de liberar todos os identificadores de conexão, o aplicativo libera o identificador de ambiente.  
  
 Um aplicativo pode se conectar a qualquer número de fontes de dados. O aplicativo pode usar uma combinação de drivers e fontes de dados, o mesmo driver e uma combinação de fontes de dados ou inclusive o mesmo driver e várias conexões com a mesma fonte de dados.  
  
 Você pode baixar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Native Client ODBC amostras do [Downloads do SQL Server](http://go.microsoft.com/fwlink/?LinkId=62796) página no MSDN.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Alocando um identificador de ambiente](allocating-an-environment-handle.md)  
  
-   [Alocando um identificador de conexão](allocating-a-connection-handle.md)  
  
-   [Fontes de dados ODBC do SQL Server Native Client](../../integration-services/connection-manager/data-sources.md)  
  
-   [Conectando a uma fonte de dados &#40;ODBC&#41;](connecting-to-a-data-source-odbc.md)  
  
-   [Desconectando uma fonte de dados](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
