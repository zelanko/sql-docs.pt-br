---
title: Fontes de dados do SQL Server Native Client ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: native-client
ms.topic: reference
helpviewer_keywords:
- ODBC data sources, about data sources
- ODBC data sources, names
- data sources [SQL Server Native Client]
- names [ODBC]
- ODBC applications, data sources
- SQL Server Native Client ODBC driver, data sources
- ODBC data sources
ms.assetid: a6a50fd0-d439-43fd-b76f-16ec02f478c5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: de1226d675859312e1ccaf908141586f865c8946
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63028383"
---
# <a name="sql-server-native-client-odbc-data-sources"></a>fontes de dados ODBC do SQL Server Native Client
  Um DSN (nome da fonte de dados) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] identifica uma fonte de dados ODBC que contém todas as informações de que um aplicativo ODBC precisa para se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor específico. Há duas maneiras de definir um nome da fonte de dados ODBC:  
  
-   Em um computador cliente, abra Ferramentas administrativas no painel de controle e clique duas vezes em **fontes de dados (ODBC)** . O Administrador de Fonte de Dados ODBC será aberto e poderá ser usado para criar um DSN.  
  
-   Em um aplicativo ODBC, chame [SQLConfigDataSource](../native-client-odbc-api/sqlconfigdatasource.md).  
  
 Uma fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] contém:  
  
-   O nome da fonte de dados.  
  
-   Quaisquer informações necessárias para se conectar a uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   O banco de dados padrão a ser usado em uma instância específica do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (opcional).  
  
-   Configurações como quais opções ANSI serão usadas, se as estatísticas de desempenho serão registradas ou não e assim por diante (opcional).  
  
 Não é necessário um aplicativo ODBC para se conectar através de uma fonte de dados. Entretanto, o aplicativo precisa fornecer as mesmas informações de conectividade para uma função de conexão ODBC que de outro modo o driver encontraria em um DSN.  
  
## <a name="see-also"></a>Consulte também  
 [Comunicando-se com o SQL Server &#40;ODBC&#41;](communicating-with-sql-server-odbc.md)  
  
  
