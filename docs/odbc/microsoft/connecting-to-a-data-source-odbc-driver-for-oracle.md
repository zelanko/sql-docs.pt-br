---
title: Conectando a uma fonte de dados (ODBC Driver for Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
caps.latest.revision: 10
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7c12472544fd843214cab4294311889d0a84010d
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectando a uma fonte de dados (ODBC Driver for Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Um aplicativo ODBC pode transmitir informações de conexão de várias maneiras. Por exemplo, o aplicativo pode ter o driver sempre solicitar ao usuário informações de conexão. Ou o aplicativo pode esperar uma cadeia de caracteres de conexão que especifica a conexão de fonte de dados. Como se conectar a uma fonte de dados depende do método de conexão usado pelo seu aplicativo de ODBC.  
  
 Uma maneira comum para se conectar a uma fonte de dados é através da caixa de diálogo de fonte de dados. Se seu aplicativo ODBC estiver configurado para usar uma caixa de diálogo, caixa de diálogo é exibida e solicita as informações de conexão de fonte de dados apropriado.  
  
 Você também pode se conectar a uma fonte de dados usando o [cadeia de caracteres de conexão](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para se conectar a uma fonte de dados usando uma caixa de diálogo  
  
1.  Quando for exibida a caixa de diálogo de fonte de dados, selecione uma fonte de dados Oracle e clique em Okey. Caixa de diálogo é exibida.  
  
2.  Preencha as informações apropriadas para a caixa de diálogo Conectar e, em seguida, clique em Okey.  
  
 Após a conexão é verificar as informações, seu aplicativo pode usar o Driver ODBC do Oracle para acessar as informações que contém a fonte de dados.
