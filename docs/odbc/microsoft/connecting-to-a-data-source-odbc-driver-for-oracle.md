---
title: Conectando-se a uma fonte de dados (Driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6ef567c9e3c7b63e7f5044de699750de856f3e52
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281296"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectar-se a uma fonte de dados (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Um aplicativo ODBC pode passar informações de conexão de várias maneiras. Por exemplo, o aplicativo pode ter o driver sempre solicitar ao usuário informações de conexão. Ou o aplicativo pode esperar uma seqüência de conexão que especifique a conexão de origem de dados. A forma como você se conecta a uma fonte de dados depende do método de conexão usado pelo aplicativo ODBC.  
  
 Uma maneira comum de se conectar a uma fonte de dados é através da caixa de diálogo Fonte de dados. Se o aplicativo ODBC estiver configurado para usar uma caixa de diálogo, essa caixa de diálogo será exibida e solicitará informações apropriadas sobre a conexão de origem de dados.  
  
 Você também pode se conectar a uma fonte de dados usando a [seqüência de conexões](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para se conectar a uma fonte de dados usando uma caixa de diálogo  
  
1.  Quando a caixa de diálogo Fonte de dados aparecer, selecione uma fonte de dados Oracle e clique em OK. A caixa de diálogo Conectar é exibida.  
  
2.  Preencha as informações apropriadas para a caixa de diálogo Conectar e clique em OK.  
  
 Depois que as informações de conexão forem verificadas, seu aplicativo pode usar o Driver ODBC para Oracle para acessar as informações que a fonte de dados contém.
