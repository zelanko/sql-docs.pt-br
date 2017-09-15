---
title: "Etapa 1: Conectar-se à fonte de dados | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application process [ODBC], connecting to data source
- data sources [ODBC], connections
- connecting to data source [ODBC], steps
ms.assetid: 84298664-4523-4149-b821-7b2e42c85281
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 42da1bad914342a2f2973a63dc35f6e53f8b6c93
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="step-1-connect-to-the-data-source"></a>Etapa 1: Conectar-se à fonte de dados
É a primeira etapa em qualquer aplicativo para se conectar à fonte de dados. Nesta fase, incluindo as funções requer, é mostrada na ilustração a seguir.  
  
 ![Conectar-se à fonte de dados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 A primeira etapa na conexão à fonte de dados é carregar o Gerenciador de Driver e alocar o identificador de ambiente com **SQLAllocHandle**. Para obter mais informações, consulte [ao alocar identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em seguida, o aplicativo registra a versão do ODBC para o qual ele está em conformidade chamando **SQLSetEnvAttr** com o atributo de ambiente SQL_ATTR_APP_ODBC_VER. Para obter mais informações, consulte [declarar a versão do aplicativo ODBC](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [compatibilidade com versões anteriores e a conformidade com padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Em seguida, o aplicativo aloca um identificador de conexão com **SQLAllocHandle** e conecta-se à fonte de dados com **SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**. Para obter mais informações, consulte [alocar um identificador de Conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) e [estabelecer uma Conexão](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 Em seguida, o aplicativo define os atributos de conexão, como confirmar manualmente transações. Para obter mais informações, consulte [atributos de Conexão](../../../odbc/reference/develop-app/connection-attributes.md).
