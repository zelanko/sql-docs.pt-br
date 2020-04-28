---
title: Recuperando informações de tipo de dados com SQLGetTypeInfo | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300056"
---
# <a name="retrieving-data-type-information-with-sqlgettypeinfo"></a>Recuperar informações de tipo de dados com SQLGetTypeInfo
Como os mapeamentos de tipos de dados SQL subjacentes para identificadores de tipo ODBC são aproximados, o ODBC fornece uma função (**SQLGetTypeInfo**) por meio da qual um driver pode descrever completamente cada tipo de dados SQL na fonte de dados. Essa função retorna um conjunto de resultados, cada linha que descreve as características de um único tipo de dados, como nome, identificador de tipo, precisão, escala e nulidade.  
  
 Essas informações geralmente são usadas por aplicativos genéricos que permitem ao usuário criar e alterar tabelas. Esses aplicativos chamam **SQLGetTypeInfo** para recuperar as informações de tipo de dados e, em seguida, apresentar algumas ou todas elas ao usuário. Esses aplicativos precisam estar cientes de duas coisas:  
  
-   Mais de um tipo de dados SQL pode ser mapeado para um único identificador de tipo, o que pode dificultar a determinação do tipo de dados a ser usado. Para resolver isso, o conjunto de resultados é ordenado primeiro pelo identificador de tipo e segundo por proximidade com a definição do identificador de tipo. Além disso, os tipos de dados definidos pela fonte de dados têm precedência sobre os tipos de dados definidos pelo usuário. Por exemplo, suponha que uma fonte de dados defina os tipos de dados INTEGER e COUNTER como o mesmo, exceto que o contador é incrementado automaticamente. Suponha também que o tipo definido pelo usuário WHOLENUM é um sinônimo de inteiro. Cada um desses tipos é mapeado para SQL_INTEGER. No conjunto de resultados **SQLGetTypeInfo** , Integer aparece primeiro, seguido por WHOLENUM e, em seguida, Counter. WHOLENUM aparece depois de INTEGER porque é definido pelo usuário, mas antes do contador porque ele corresponde mais próximo à definição do identificador de tipo de SQL_INTEGER.  
  
-   O ODBC não define nomes de tipos de dados para uso em instruções **CREATE TABLE** e **ALTER TABLE** . Em vez disso, o aplicativo deve usar o nome retornado na coluna TYPE_NAME do conjunto de resultados retornado por **SQLGetTypeInfo**. O motivo disso é que, embora a maior parte do SQL não varie muito em DBMSs, os nomes de tipos de dados variam enormemente. Em vez de forçar os drivers a analisar instruções SQL e substituir nomes de tipo de dados padrão por nomes de tipo de dados específicos do DBMS, o ODBC requer que os aplicativos usem os nomes específicos do DBMS em primeiro lugar.  
  
 Observe que o **SQLGetTypeInfo** não descreve necessariamente todos os tipos de dados que um aplicativo pode encontrar. Em particular, os conjuntos de resultados podem conter tipos de dados não suportados diretamente pela fonte de dados. Por exemplo, os tipos de dados das colunas nos conjuntos de resultados retornados pelas funções de catálogo são definidos pelo ODBC e esses tipos de dados podem não ser suportados pela fonte de dados. Para determinar as características dos tipos de dados em um conjunto de resultados, um aplicativo chama **SQLColAttribute**.
