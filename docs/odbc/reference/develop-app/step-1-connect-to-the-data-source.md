---
description: 'Etapa 1: Conectar-se à fonte de dados'
title: 'Etapa 1: conectar-se à fonte de dados | Microsoft Docs'
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
ms.openlocfilehash: 9ac15eed6c84745dca6406ad8186f14c65798939
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88482959"
---
# <a name="step-1-connect-to-the-data-source"></a>Etapa 1: Conectar-se à fonte de dados
A primeira etapa em qualquer aplicativo é conectar-se à fonte de dados. Essa fase, incluindo as funções necessárias, é mostrada na ilustração a seguir.  
  
 ![Conexão com a fonte de dados em um aplicativo ODBC](../../../odbc/reference/develop-app/media/pr11.gif "pr11")  
  
 A primeira etapa na conexão à fonte de dados é carregar o Gerenciador de driver e alocar o identificador de ambiente com **SQLAllocHandle**. Para obter mais informações, consulte [alocando o identificador de ambiente](../../../odbc/reference/develop-app/allocating-the-environment-handle.md).  
  
 Em seguida, o aplicativo registra a versão do ODBC à qual ele está de acordo chamando **SQLSetEnvAttr** com o atributo de ambiente SQL_ATTR_APP_ODBC_VER. Para obter mais informações, consulte [declarando a versão do ODBC do aplicativo](../../../odbc/reference/develop-app/declaring-the-application-s-odbc-version.md) e [compatibilidade com versões anteriores e conformidade de padrões](../../../odbc/reference/develop-app/backward-compatibility-and-standards-compliance.md).  
  
 Em seguida, o aplicativo aloca um identificador de conexão com **SQLAllocHandle** e conecta-se à fonte de dados com **SQLConnect**, **SQLDriverConnect**ou **SQLBrowseConnect**. Para obter mais informações, consulte [alocando um identificador de conexão](../../../odbc/reference/develop-app/allocating-a-connection-handle-odbc.md) e [estabelecendo uma conexão](../../../odbc/reference/develop-app/establishing-a-connection.md).  
  
 Em seguida, o aplicativo define qualquer atributo de conexão, por exemplo, se as transações devem ser confirmadas manualmente. Para obter mais informações, consulte [atributos de conexão](../../../odbc/reference/develop-app/connection-attributes.md).
