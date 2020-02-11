---
title: Fonte de dados padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- connecting to data source [ODBC], default data source
- functions [ODBC], data source or driver connections
- data sources [ODBC], default
- default data source [ODBC]
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], default data source
- connecting to driver [ODBC], functions
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: dd473cc6-f051-4aa0-ab14-3dd1b37fe99e
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 8fb016ac7597617b119834e20ffd9e12bd648dc0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076859"
---
# <a name="default-data-source"></a>Fonte de dados padrão
O driver pode selecionar uma fonte de dados, chamada de fonte de dados padrão, em determinados casos em que o aplicativo não especifica explicitamente uma:  
  
-   Em uma chamada para **SQLConnect** , onde o argumento *ServerName* é uma cadeia de caracteres de comprimento zero, um ponteiro nulo ou um padrão.  
  
-   Em uma chamada para **SQLDriverConnect** em que *inconnectionstring* especifica **DSN**= Default ou especifica com a palavra-chave **DSN** uma fonte de dados que não está contida nas informações do sistema.  
  
 Ele é definido por driver como a fonte de dados padrão é especificada. Isso pode envolver a ação administrativa e pode depender do usuário.
