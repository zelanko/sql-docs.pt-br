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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 978362b7dfe92d1333f83be684f6326cf25dd69b
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305987"
---
# <a name="default-data-source"></a>Fonte de dados padrão
O driver pode selecionar uma fonte de dados, chamada fonte de dados padrão, em certos casos em que o aplicativo não especifica explicitamente um:  
  
-   Em uma chamada para **SQLConnect,** onde o argumento *ServerName* é uma seqüência de comprimento zero, um ponteiro nulo ou PADRÃO.  
  
-   Em uma chamada para **SQLDriverConnect** onde *o InConnectionString* especifica **DSN**=DEFAULT ou especifica com a palavra-chave **DSN** uma fonte de dados que não está contida nas informações do sistema.  
  
 É definido pelo driver como a fonte de dados padrão é especificada. Isso pode envolver ação administrativa e pode depender do usuário.
