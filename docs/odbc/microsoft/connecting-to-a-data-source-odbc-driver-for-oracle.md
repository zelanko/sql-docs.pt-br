---
title: Conectando-se a uma fonte de dados (driver ODBC para Oracle) | Microsoft Docs
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
ms.openlocfilehash: b0e9e62c8e03166ec2f76b1c6bcb5000a062bac3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68082045"
---
# <a name="connecting-to-a-data-source-odbc-driver-for-oracle"></a>Conectar-se a uma fonte de dados (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Um aplicativo ODBC pode passar informações de conexão de várias maneiras. Por exemplo, o aplicativo pode ter o driver sempre solicitar informações de conexão ao usuário. Ou o aplicativo pode esperar uma cadeia de conexão que especifica a conexão da fonte de dados. A maneira como você se conecta a uma fonte de dados depende do método de conexão usado pelo seu aplicativo ODBC.  
  
 Uma maneira comum de se conectar a uma fonte de dados é por meio da caixa de diálogo fonte de dados. Se seu aplicativo ODBC estiver configurado para usar uma caixa de diálogo, essa caixa de diálogo será exibida e solicitará as informações de conexão da fonte de dados apropriada.  
  
 Você também pode se conectar a uma fonte de dados usando a [cadeia de conexão](../../odbc/microsoft/connection-string-format-and-attributes.md).  
  
### <a name="to-connect-to-a-data-source-using-a-dialog-box"></a>Para se conectar a uma fonte de dados usando uma caixa de diálogo  
  
1.  Quando a caixa de diálogo fonte de dados for exibida, selecione uma fonte de dados Oracle e clique em OK. A caixa de diálogo Conectar é exibida.  
  
2.  Preencha as informações apropriadas para a caixa de diálogo conectar e clique em OK.  
  
 Depois que as informações de conexão são verificadas, seu aplicativo pode usar o driver ODBC para Oracle para acessar as informações contidas na fonte de dados.
