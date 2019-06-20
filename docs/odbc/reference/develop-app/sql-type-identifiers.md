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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 1763ee0cd8c5bc2017160de44b9c047781649eba
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63150027"
---
# <a name="sql-type-identifiers"></a>Identificadores de tipo SQL
Cada fonte de dados define seus próprios tipos de dados SQL. ODBC define os identificadores de tipo e descreve as características gerais dos tipos de dados SQL que podem ser mapeados para cada identificador de tipo. Ela é específica do driver como cada tipo de dados na fonte de dados subjacente é mapeado para um identificador de tipo SQL do ODBC.  
  
 Por exemplo, SQL_CHAR é o identificador de tipo para uma coluna de caractere com um comprimento fixo, normalmente entre 1 e 254 caracteres. Essas características correspondem ao tipo de dados CHAR, encontrado em várias fontes de dados SQL. Assim, quando um aplicativo descobre que o identificador de tipo para uma coluna é SQL_CHAR, ele pode assumir que provavelmente está lidando com uma coluna CHAR. No entanto, ainda deve verificar o tamanho de bytes da coluna antes de assumir que ele está entre 1 e 254 caracteres; o driver para uma fonte de dados não-SQL, por exemplo, pode mapear uma coluna de caracteres de comprimento fixo de 500 caracteres para SQL_CHAR ou SQL_LONGVARCHAR, porque nenhum dos dois é uma correspondência exata.  
  
 ODBC define uma ampla variedade de identificadores de tipo SQL. No entanto, o driver não é necessário usar todos esses identificadores. Em vez disso, ele usa apenas esses identificadores que ele precisa expor os tipos de dados SQL com suporte pela fonte de dados subjacente. Se a fonte de dados subjacente der suporte a tipos de dados SQL para que nenhum identificador de tipo corresponde, o driver pode definir identificadores de tipo adicionais. Para obter mais informações, consulte [tipos de dados específicos do Driver, tipos de descritor, tipos de informação, tipos de diagnóstico e atributos](../../../odbc/reference/develop-app/driver-specific-data-types-descriptor-information-diagnostic.md).  
  
 Para obter uma descrição completa de identificadores de tipo SQL, consulte [tipos de dados C](../../../odbc/reference/appendixes/c-data-types.md) no Apêndice d: Tipos de dados.
