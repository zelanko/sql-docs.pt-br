---
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
ms.openlocfilehash: 95bf46844e9ed91aac1ec6cb93a298995f0901d6
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299766"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada fonte de dados define seus próprios tipos de dados SQL. O ODBC define identificadores de tipo e descreve as características gerais dos tipos de dados SQL que podem ser mapeadas para cada identificador de tipo. É específico do driver como cada tipo de dados na fonte de dados subjacente é mapeado para um identificador do tipo SQL do ODBC.  
  
 Por exemplo, SQL_CHAR é o identificador de tipo para uma coluna de caracteres com um comprimento fixo, tipicamente entre 1 e 254 caracteres. Essas características correspondem ao tipo de dados CHAR encontrado em muitas fontes de dados SQL. Assim, quando um aplicativo descobre que o identificador de tipo para uma coluna é SQL_CHAR, ele pode assumir que provavelmente está lidando com uma coluna CHAR. No entanto, ele ainda deve verificar o comprimento do byte da coluna antes de assumir que está entre 1 e 254 caracteres; o driver para uma fonte de dados não-SQL, por exemplo, pode mapear uma coluna de caracteres de comprimento fixo de 500 caracteres para SQL_CHAR ou SQL_LONGVARCHAR, porque nenhum deles é uma correspondência exata.  
  
 O ODBC define uma grande variedade de identificadores do tipo SQL. No entanto, o motorista não é obrigado a usar todos esses identificadores. Em vez disso, ele usa apenas os identificadores necessários para expor os tipos de dados SQL suportados pela fonte de dados subjacente. Se a fonte de dados subjacente suportar tipos de dados SQL aos quais nenhum identificador de tipo corresponde, o driver poderá definir identificadores adicionais de tipo. Para obter mais informações, consulte [tipos de dados específicos do driver, tipos de descritores, tipos de informações, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obter uma descrição completa dos identificadores do tipo SQL, consulte [C Data Types](../../../odbc/reference/appendixes/c-data-types.md) in Apêndice D: Data Types.
