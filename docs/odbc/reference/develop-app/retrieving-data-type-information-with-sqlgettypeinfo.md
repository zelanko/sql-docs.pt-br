---
title: Recuperar dados de tipo de informações com SQLGetTypeInfo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- SQL data types [ODBC], identifiers
- SQLGetTypeInfo function [ODBC], retrieving data type information
- retrieving data type information [ODBC]
- type identifiers [ODBC], SQL
- identifiers [ODBC], SQL type
- SQL type identifiers [ODBC]
ms.assetid: d4f8b152-ab9e-4d05-a720-d10a08a6df81
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: d764d8470343d67bd37c1ef7ce5dcf15962079e9
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recuperar informações de tipo de dados com SQLGetTypeInfo
Como os mapeamentos de tipos de dados SQL subjacentes para identificadores de tipo ODBC são aproximados, ODBC fornece uma função (**SQLGetTypeInfo**) por meio do qual um driver pode completamente descrevem cada tipo de dados SQL na fonte de dados. Essa função retorna um conjunto de resultados, cada linha que descreve as características de um tipo de dados simples, como nome, tipo de identificador, precisão, escala e nulidade.  
  
 Geralmente, essas informações são usadas por aplicativos genéricos que permitem ao usuário criar e alterar tabelas. Esse aplicativos chamam **SQLGetTypeInfo** para recuperar as informações de tipo de dados e, em seguida, exibe alguns ou todos eles para o usuário. Esses aplicativos precisam estar ciente das seguintes ações:  
  
-   Mais de um tipo de dados SQL pode mapear para um identificador de tipo simples, que pode tornar difícil determinar qual tipo de dados a ser usado. Para resolver isso, o conjunto de resultados é ordenado pela primeira vez pelo identificador de tipo e depois pela proximidade à definição do identificador de tipo. Além disso, tipos de dados definidos para fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Por exemplo, suponha que uma fonte de dados define os tipos de dados inteiro e um CONTADOR para ser o mesmo, exceto que o CONTADOR é incremento automático. Suponha também que o tipo definido pelo usuário WHOLENUM é um sinônimo de número inteiro. Cada um desses tipos de mapas para SQL_INTEGER. No **SQLGetTypeInfo** conjunto de resultados, inteiro aparece primeiro, seguido por WHOLENUM e, em seguida, o CONTADOR. WHOLENUM aparece depois inteiro porque ele é definido pelo usuário, mas antes de CONTADOR porque ele mais se aproxima a definição do SQL_INTEGER tipo identificador.  
  
-   ODBC não define os nomes de tipo de dados para uso em **CREATE TABLE** e **ALTER TABLE** instruções. Em vez disso, o aplicativo deve usar o nome retornado na coluna TYPE_NAME do conjunto de resultados retornado por **SQLGetTypeInfo**. O motivo disso é que embora a maioria do SQL variam muito em DBMSs, nomes de tipo de dados podem variar muito. Em vez de forçá-drivers para analisar instruções SQL e substitua os nomes de tipo de dados padrão com nomes de tipo de dados DBMS específico, o ODBC requer aplicativos para usar os nomes de DBMS específico em primeiro lugar.  
  
 Observe que **SQLGetTypeInfo** não necessariamente descreve todos os tipos de dados pode encontrar um aplicativo. Em particular, os conjuntos de resultados podem conter tipos de dados sem suporte direto a fonte de dados. Por exemplo, os tipos de dados das colunas em conjuntos de resultados retornados pelas funções de catálogo são definidos pelo ODBC e esses tipos de dados talvez não tenha suporte pela fonte de dados. Para determinar as características dos tipos de dados em um conjunto de resultados, um aplicativo chama **SQLColAttribute**.
