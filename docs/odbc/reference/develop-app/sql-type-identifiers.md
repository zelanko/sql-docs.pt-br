---
description: Identificadores de tipo SQL
title: Identificadores de tipo SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], identifiers
- SQL data types [ODBC], identifiers
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: 22f6793b-2f43-4281-b35a-28f48e504dd8
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 211cfdbe7805bade2875723a1cb62a02b5c876d3
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424508"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada fonte de dados define seus próprios tipos de dados SQL. O ODBC define identificadores de tipo e descreve as características gerais dos tipos de dados SQL que podem ser mapeados para cada identificador de tipo. Ele é específico ao driver, como cada tipo de dados na fonte de dados subjacente é mapeado para um identificador de tipo SQL do ODBC.  
  
 Por exemplo, SQL_CHAR é o identificador de tipo para uma coluna de caracteres com um comprimento fixo, normalmente entre 1 e 254 caracteres. Essas características correspondem ao tipo de dados CHAR encontrado em muitas fontes de dados SQL. Assim, quando um aplicativo descobre que o identificador de tipo de uma coluna é SQL_CHAR, ele pode pressupor que provavelmente está lidando com uma coluna CHAR. No entanto, ele ainda deve verificar o comprimento de bytes da coluna antes de presumir que esteja entre 1 e 254 caracteres; o driver para uma fonte de dados não SQL, por exemplo, pode mapear uma coluna de caracteres de comprimento fixo de 500 caracteres para SQL_CHAR ou SQL_LONGVARCHAR, porque nenhuma delas é uma correspondência exata.  
  
 O ODBC define uma ampla variedade de identificadores de tipo SQL. No entanto, o driver não é necessário para usar todos esses identificadores. Em vez disso, ele usa apenas os identificadores necessários para expor os tipos de dados SQL com suporte na fonte de dados subjacente. Se a fonte de dados subjacente oferecer suporte a tipos de dados SQL aos quais nenhum identificador de tipo corresponde, o driver poderá definir identificadores de tipo adicionais. Para obter mais informações, consulte [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obter uma descrição completa dos identificadores de tipo SQL, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice D: tipos de dados.
