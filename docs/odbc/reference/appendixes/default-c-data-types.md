---
title: Padrão de tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9c4147b1bfa5ffb1e379c3aa8be2c9ea2a9d2775
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63240964"
---
# <a name="default-c-data-types"></a>Tipos de dados do C padrão
Se um aplicativo especifica SQL_C_DEFAULT na **SQLBindCol**, **SQLGetData**, ou **SQLBindParameter**, o driver pressupõe que o C tipo de dados do buffer de entrada ou saída corresponde ao tipo de dados SQL da coluna ou parâmetro ao qual o buffer está associado.  
  
> [!IMPORTANT]  
>  Aplicativos interoperáveis não devem usar SQL_C_DEFAULT. Em vez disso, eles sempre devem especificar o tipo C de buffer que estiverem usando. Isso ocorre porque os drivers sempre corretamente não é possível determinar o tipo de C padrão, pelos seguintes motivos:  
  
-   Se o DBMS promove um tipo de dados SQL de uma coluna ou parâmetro, o driver não pode determinar o tipo de dados SQL original de uma coluna ou parâmetro. Portanto, ele não é possível determinar o tipo de dados C padrão correspondente.  
  
-   Se o driver não pode determinar se uma determinada coluna ou parâmetro está assinado, pois geralmente é o caso quando se trata manipulados pelo DBMS, o driver não pode determinar se os dados correspondentes do C padrão tipo deve ser assinado ou não assinado.  
  
     Como SQL_C_DEFAULT é fornecida apenas como uma conveniência de programação, o aplicativo não perderá qualquer funcionalidade quando ela especifica o tipo de dados real do C.  
  
 Uma tabela que mostra o tipo de dados C padrão para cada tipo de dados SQL está incluída no [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), mais adiante neste apêndice.
