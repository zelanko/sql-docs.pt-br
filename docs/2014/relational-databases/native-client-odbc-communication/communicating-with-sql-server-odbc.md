---
title: Comunicando-se com SQL Server (ODBC) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- SQL Server Native Client ODBC driver, communicating with SQL Server
- ODBC applications, communicating with SQL Server
- ODBC, communicating with SQL Server
ms.assetid: cca3dcf0-2a7e-465a-84de-7ce055360eb6
author: rothja
ms.author: jroth
ms.openlocfilehash: c41ac2dcce9c5bdbdd351148d16bcaa8f067d22f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85021197"
---
# <a name="communicating-with-sql-server-odbc"></a>Comunicando-se com o SQL Server (ODBC)
  Para que um aplicativo ODBC se comunique com uma instância do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , ele deve alocar identificadores de ambiente e conexão e conectar-se à fonte de dados. Depois que uma conexão é estabelecida, o aplicativo pode enviar consultas ao servidor e processar quaisquer conjuntos de resultados. Quando o aplicativo conclui o uso da fonte de dados, ele se desconecta da fonte de dados e libera o identificador de conexão. Depois de liberar todos os identificadores de conexão, o aplicativo libera o identificador de ambiente.  
  
 Um aplicativo pode se conectar a qualquer número de fontes de dados. O aplicativo pode usar uma combinação de drivers e fontes de dados, o mesmo driver e uma combinação de fontes de dados ou inclusive o mesmo driver e várias conexões com a mesma fonte de dados.  
  
 Você pode baixar [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] exemplos de ODBC de cliente nativo na página de [Downloads de SQL Server](https://go.microsoft.com/fwlink/?LinkId=62796) no msdn.  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Alocando um identificador de ambiente](allocating-an-environment-handle.md)  
  
-   [Alocando um identificador de conexão](allocating-a-connection-handle.md)  
  
-   [fontes de dados ODBC do SQL Server Native Client](../../integration-services/connection-manager/data-sources.md)  
  
-   [Conectando-se a uma fonte de dados &#40;&#41;ODBC](connecting-to-a-data-source-odbc.md)  
  
-   [Desconectando uma fonte de dados](disconnecting-from-a-data-source.md)  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Native Client &#40;ODBC&#41;](../native-client/odbc/sql-server-native-client-odbc.md)   
 [SQLSetEnvAttr](../native-client-odbc-api/sqlsetenvattr.md)  
  
  
