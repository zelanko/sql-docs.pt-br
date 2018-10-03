---
title: 'Etapa 1: Conectar-se à fonte de dados | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 154fdd7368835ba2a578d3ec641705c4064859ac
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47600894"
---
# <a name="step-1-connect-to-the-data-source"></a>Etapa 1: Conectar-se à fonte de dados
É a primeira etapa em qualquer aplicativo para se conectar à fonte de dados. Nesta fase, incluindo as funções que requer, é mostrada na ilustração a seguir.  
  
 ![Conectar-se à fonte de dados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 A primeira etapa ao conectar-se à fonte de dados é carregar o Gerenciador de Driver e alocar o identificador de ambiente com **SQLAllocHandle**. Para obter mais informações, consulte [alocar o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 O aplicativo, em seguida, registra a versão do ODBC para o qual ele está em conformidade com chamando **SQLSetEnvAttr** com o atributo de ambiente SQL_ATTR_APP_ODBC_VER. Para obter mais informações, consulte [declarando a versão do aplicativo ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [compatibilidade com versões anteriores e em conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Em seguida, o aplicativo aloca um identificador de conexão com **SQLAllocHandle** e conecta-se à fonte de dados com **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**. Para obter mais informações, consulte [alocando um identificador de Conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) e [estabelecendo uma Conexão](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 O aplicativo, em seguida, define os atributos de conexão, como se deve confirmar manualmente transações. Para obter mais informações, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).
