---
title: Padrão de tipos de dados C | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- data types [ODBC], pseudo-type identifiers
- pseudo-type identifiers [ODBC], about pseudo-type identifiers
- pseudo-type identifiers [ODBC]
ms.assetid: 229140ae-af8f-4ec8-9ccf-1e92360e0bac
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 730203c438568152bb1ce42ef5f152c87bd5f468
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="default-c-data-types"></a>Tipos de dados C padrão
Se um aplicativo especifica SQL_C_DEFAULT em **SQLBindCol**, **SQLGetData**, ou **SQLBindParameter**, o driver pressupõe que o C tipo de dados do buffer de entrada ou saída corresponde ao tipo de dados SQL da coluna ou parâmetro ao qual o buffer está associado.  
  
> [!IMPORTANT]  
>  Aplicativos interoperáveis não devem usar SQL_C_DEFAULT. Em vez disso, eles sempre devem especificar o tipo de C do buffer que estão usando. Isso ocorre porque os drivers corretamente não é possível determinar o tipo de C padrão, pelos seguintes motivos:  
  
-   Se o DBMS promove um tipo de dados SQL de uma coluna ou parâmetro, o driver não pode determinar o tipo de dados SQL original de uma coluna ou parâmetro. Portanto, não é possível determinar o tipo de dados C padrão correspondente.  
  
-   Se o driver não pode determinar se uma determinada coluna ou parâmetro está assinado, pois geralmente é o caso quando isso é tratado pelo DBMS, o driver não pode determinar se tipo de dados C padrão correspondentes deve ser assinado ou não assinado.  
  
     Porque SQL_C_DEFAULT é fornecido apenas como uma conveniência de programação, o aplicativo não perderá qualquer funcionalidade quando ela especifica o tipo de dados C real.  
  
 Uma tabela que mostra o tipo de dados C padrão para cada tipo de dados SQL está incluída no [conversão de dados do SQL para tipos de dados C](../../../odbc/reference/appendixes/converting-data-from-sql-to-c-data-types.md), mais adiante neste apêndice.
