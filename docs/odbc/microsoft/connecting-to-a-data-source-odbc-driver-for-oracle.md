---
title: Conectando a uma fonte de dados (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], connecting to data sources
ms.assetid: f724a9c5-342a-4f4e-a030-ec34f7378eaf
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: adee8d8dd8d6db0d79b37ff853c41e7604fe21de
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63302129"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectar-se a uma fonte de dados (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Um aplicativo ODBC pode passar informações de conexão de várias maneiras. Por exemplo, o aplicativo pode ter o driver sempre solicitar ao usuário informações de conexão. Ou, se o aplicativo esperar uma cadeia de caracteres de conexão que especifica a conexão de fonte de dados. Como você pode se conectar a uma fonte de dados depende do método de conexão usado pelo seu aplicativo de ODBC.  
  
 É uma maneira comum para se conectar a uma fonte de dados por meio da caixa de diálogo de fonte de dados. Se seu aplicativo de ODBC é configurado para usar uma caixa de diálogo, caixa de diálogo é exibida e solicitará as informações de conexão de fonte de dados apropriado.  
  
 Você também pode se conectar a uma fonte de dados usando o [cadeia de caracteres de conexão](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para se conectar a uma fonte de dados usando uma caixa de diálogo  
  
1.  Quando for exibida a caixa de diálogo de fonte de dados, selecione uma fonte de dados Oracle e, em seguida, clique em Okey. A caixa de diálogo Connect é exibida.  
  
2.  Preencha as informações apropriadas para a caixa de diálogo Conectar e, em seguida, clique em Okey.  
  
 Após a conexão informações serão verificadas, seu aplicativo pode usar o Driver ODBC para Oracle para acessar as informações que contém a fonte de dados.
