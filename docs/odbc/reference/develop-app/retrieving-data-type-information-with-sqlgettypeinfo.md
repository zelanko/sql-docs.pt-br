---
title: Recuperação de dados de tipo de informações com SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c69113e4bb5457cb997f832179e5c1aab2841d82
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63199097"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recuperar informações de tipo de dados com SQLGetTypeInfo
Como os mapeamentos de tipos de dados SQL subjacentes para identificadores de tipo ODBC são aproximados, o ODBC fornece uma função (**SQLGetTypeInfo**) por meio do qual um driver pode completamente descrevem cada tipo de dados SQL na fonte de dados. Essa função retorna um conjunto de resultados, cada linha que descreve as características de um tipo de dados único, como nome, identificador de tipo, precisão, escala e nulidade.  
  
 Em geral, essas informações são usadas por aplicativos genéricos que permitem ao usuário criar e alterar as tabelas. Tal aplicativos chamam **SQLGetTypeInfo** para recuperar as informações de tipo de dados e, em seguida, apresentar alguns ou todos eles para o usuário. Tais aplicativos precisam estar ciente das duas coisas:  
  
-   Mais de um tipo de dados SQL pode mapear para um identificador de tipo único, que pode tornar difícil determinar qual tipo de dados para usar. Para resolver isso, o conjunto de resultados é ordenado pela primeira vez pelo identificador de tipo e depois pela proximidade com a definição do identificador de tipo. Além disso, a tipos de dados definidos pelo código-fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Por exemplo, suponha que uma fonte de dados define os tipos de dados inteiro e um CONTADOR para ser o mesmo, exceto que o CONTADOR é incremento automático. Vamos supor também que o tipo definido pelo usuário WHOLENUM é um sinônimo de inteiro. Cada um desses tipos é mapeado para SQL_INTEGER. No **SQLGetTypeInfo** conjunto de resultados, inteiro aparece primeiro, seguido por WHOLENUM e, em seguida, o CONTADOR. WHOLENUM aparece após inteiro porque ele é definido pelo usuário, mas antes de CONTADOR porque ele mais se aproxima a definição do SQL_INTEGER identificador de tipo.  
  
-   ODBC não define os nomes de tipo de dados para uso em **CREATE TABLE** e **ALTER TABLE** instruções. Em vez disso, o aplicativo deve usar o nome retornado na coluna de TYPE_NAME do conjunto de resultados retornado por **SQLGetTypeInfo**. A razão para isso é que embora a maior parte do SQL não varia muito entre DBMSs, nomes de tipo de dados podem variar muito. Em vez de forçar os drivers para analisar as instruções SQL e substitua os nomes de tipo de dados padrão com nomes de tipo de dados específicos de DBMS, ODBC requer aplicativos para usar os nomes específicos de DBMS em primeiro lugar.  
  
 Observe que **SQLGetTypeInfo** não necessariamente descreve todos os tipos de dados, um aplicativo pode se deparar. Em particular, os conjuntos de resultados podem conter tipos de dados não é diretamente compatível com a fonte de dados. Por exemplo, os tipos de dados das colunas em conjuntos de resultados retornados pelas funções de catálogo são definidos pelo ODBC e esses tipos de dados talvez não tenha suporte pela fonte de dados. Para determinar as características dos tipos de dados em um conjunto de resultados, um aplicativo chama **SQLColAttribute**.
