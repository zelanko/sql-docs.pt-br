---
title: Recuperando informações do tipo de dados com SQLGetTypeInfo | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 4ec2bbba824eaf3d74133cf9754eca2593c9fb79
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300056"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recuperar informações de tipo de dados com SQLGetTypeInfo
Como os mapeamentos dos tipos de dados SQL subjacentes aos identificadores de tipo ODBC são aproximados, o ODBC fornece uma função (**SQLGetTypeInfo**) através da qual um driver pode descrever completamente cada tipo de dados SQL na fonte de dados. Esta função retorna um conjunto de resultados, cada linha que descreve as características de um único tipo de dados, como nome, identificador de tipo, precisão, escala e nulidade.  
  
 Essas informações geralmente são usadas por aplicativos genéricos que permitem ao usuário criar e alterar tabelas. Esses aplicativos chamam **o SQLGetTypeInfo** para recuperar as informações do tipo de dados e, em seguida, apresentar algumas ou todas elas ao usuário. Tais aplicações precisam estar cientes de duas coisas:  
  
-   Mais de um tipo de dados SQL pode mapear para um único identificador de tipo, o que pode dificultar a determinação de qual tipo de dados usar. Para resolver isso, o conjunto de resultados é ordenado primeiro por identificador de tipo e segundo pela proximidade com a definição do identificador de tipo. Além disso, os tipos de dados definidos por origem de dados têm precedência sobre os tipos de dados definidos pelo usuário. Por exemplo, suponha que uma fonte de dados define os tipos de dados INTEGER e COUNTER como sendo os mesmos, exceto que o COUNTER está incrementando automaticamente. Suponha também que o tipo definido pelo usuário WHOLENUM é um sinônimo de INTEGER. Cada um desses tipos mapeia para SQL_INTEGER. No conjunto de resultados **SQLGetTypeInfo,** INTEGER aparece primeiro, seguido por WHOLENUM e, em seguida, COUNTER. WHOLENUM aparece depois do INTEGER porque é definido pelo usuário, mas antes do COUNTER porque ele corresponde mais de perto à definição do identificador de tipo SQL_INTEGER.  
  
-   A ODBC não define nomes de tipos de dados para uso nas instruções **DE TABELA DE** CRIAÇÃO e TABELA **ALTER.** Em vez disso, o aplicativo deve usar o nome retornado na coluna TYPE_NAME do conjunto de resultados retornado pelo **SQLGetTypeInfo**. A razão para isso é que, embora a maioria do SQL não varie muito entre DBMSs, os nomes de tipo de dados variam tremendamente. Em vez de forçar os drivers a analisar as instruções SQL e substituir nomes de tipo de dados padrão por nomes de tipo de dados específicos do DBMS, o ODBC exige que os aplicativos usem os nomes específicos do DBMS em primeiro lugar.  
  
 Observe que **o SQLGetTypeInfo** não descreve necessariamente todos os tipos de dados que um aplicativo pode encontrar. Em particular, os conjuntos de resultados podem conter tipos de dados não suportados diretamente pela fonte de dados. Por exemplo, os tipos de dados das colunas nos conjuntos de resultados retornados pelas funções do catálogo são definidos pela ODBC e esses tipos de dados podem não ser suportados pela fonte de dados. Para determinar as características dos tipos de dados em um conjunto de resultados, um aplicativo chama **SQLColAttribute**.
