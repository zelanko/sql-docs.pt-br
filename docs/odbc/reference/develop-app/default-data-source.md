---
title: Padrão de fonte de dados | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 909f9b3e7c8087add8eb66ca2f5c15253026304c
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47619564"
---
# <a name="default-data-source"></a>Fonte de dados padrão
O driver pode selecionar uma fonte de dados, chamada de fonte de dados padrão, em certos casos em que o aplicativo não especificar explicitamente um:  
  
-   Em uma chamada para **SQLConnect** em que o *ServerName* argumento é uma cadeia de caracteres de comprimento zero, um ponteiro nulo ou padrão.  
  
-   Em uma chamada para **SQLDriverConnect** onde *InConnectionString* o especifica **DSN**= padrão ou especifica com o **DSN** palavra-chave um fonte de dados que não está contido nas informações do sistema.  
  
 Ele é definido pelo driver como a fonte de dados padrão é especificada. Isso pode envolver a ação administrativa e pode depender do usuário.
