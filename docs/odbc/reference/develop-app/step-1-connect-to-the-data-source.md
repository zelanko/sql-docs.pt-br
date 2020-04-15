---
title: 'Passo 1: Conecte-se à fonte de dados | Microsoft Docs'
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2a104733c0e5ec5acc87eeabd00c4e51d4bfd000
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301346"
---
# <a name="step-1-connect-to-the-data-source"></a>Etapa 1: Conectar-se à fonte de dados
O primeiro passo em qualquer aplicativo é conectar-se à fonte de dados. Esta fase, incluindo as funções necessárias, é mostrada na ilustração a seguir.  
  
 ![Conexão com a fonte de dados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 O primeiro passo para se conectar à fonte de dados é carregar o Driver Manager e alocar a alça do ambiente com **sqlallocHandle**. Para obter mais informações, consulte [Alocando a alça do ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em seguida, o aplicativo registra a versão do ODBC à qual ele se conforma chamando **sqlsetenvAttr** com o atributo ambiente SQL_ATTR_APP_ODBC_VER. Para obter mais informações, consulte [Declarando a versão ODBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [conformidade com a compatibilidade e padrões atrasados](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md)do aplicativo.  
  
 Em seguida, o aplicativo aloca uma alça de conexão com **o SQLAllocHandle** e se conecta à fonte de dados com **SQLConnect,** **SQLDriverConnect**ou **SQLBrowseConnect**. Para obter mais informações, consulte [Alocar uma alça de conexão e](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) [estabelecer uma conexão](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 Em seguida, o aplicativo define quaisquer atributos de conexão, como se deve cometer transações manualmente. Para obter mais informações, consulte [Atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).
