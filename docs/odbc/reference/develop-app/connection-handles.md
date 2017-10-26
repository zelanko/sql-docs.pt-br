---
title: "Identificadores de Conexão | Microsoft Docs"
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
- connection handles [ODBC]
- handles [ODBC], connection
ms.assetid: 12222653-f04d-46d6-bdee-61348f5d550f
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ba20d3fcb6d943f4669774013dcb62c8ad896d8d
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="connection-handles"></a>Identificadores de Conexão
Um *conexão* consiste em um driver e uma fonte de dados. Um identificador de conexão identifica cada conexão. O identificador de conexão define não qual driver usar apenas a fonte de dados para usar com esse driver. Dentro de um segmento de código que implementa ODBC (o Gerenciador de Driver ou um driver), o identificador de conexão identifica uma estrutura que contém informações de conexão, como o seguinte:  
  
-   O estado da conexão  
  
-   O diagnóstico de nível de conexão atuais  
  
-   Os identificadores de instruções e descritores alocados no momento em que a conexão  
  
-   As configurações atuais de cada atributo de conexão  
  
 ODBC não impede que várias conexões simultâneas, se o driver oferece suporte a eles. Portanto, em um ambiente de ODBC específico, vários identificadores de conexão podem apontar para uma variedade de drivers e fontes de dados para o mesmo driver e uma variedade de fontes de dados, ou até mesmo várias conexões com o mesmo driver e a fonte de dados. Alguns drivers de limitam o número de conexões ativas, que eles oferecem suporte; opção o SQL_MAX_DRIVER_CONNECTIONS **SQLGetInfo** Especifica quantas conexões ativas que oferece suporte a um driver específico.  
  
 Identificadores de Conexão são usadas principalmente ao conectar-se à fonte de dados (**SQLConnect**, **SQLDriverConnect**, ou **SQLBrowseConnect**), desconectar-se de que os dados fonte (**SQLDisconnect**), obtendo informações sobre o driver e fonte de dados (**SQLGetInfo**), recuperando diagnóstico (**SQLGetDiagField** e **SQLGetDiagRec**) e a execução de transações (**SQLEndTran**). Eles também são usados quando a configuração e Obtendo atributos de conexão (**SQLSetConnectAttr** e **SQLGetConnectAttr**) e ao obter o formato nativo de uma instrução SQL (**SQLNativeSql **).  
  
 Identificadores de Conexão são alocados com **SQLAllocHandle** e liberadas com **SQLFreeHandle**.

