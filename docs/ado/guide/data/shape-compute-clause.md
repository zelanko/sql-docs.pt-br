---
title: Cláusula de computação de forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
author: rothja
ms.author: jroth
ms.openlocfilehash: 44ccd2c978cb0356a2fcab75daa860db0f4f77f5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760842"
---
# <a name="shape-compute-clause"></a>Cláusula COMPUTE de forma
Uma cláusula de computação de forma gera um **conjunto de registros**pai, cujas colunas consistem em uma referência ao conjunto de **registros**filho; colunas opcionais cujo conteúdo são colunas de capítulo, novo ou calculadas ou o resultado da execução de funções de agregação no **conjunto de registros** filho ou em um **conjunto de registros**com formato anterior; e quaisquer colunas do conjunto de **registros** filho listadas na cláusula opcional by.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Descrição  
 As partes dessa cláusula são as seguintes:  
  
 *child-command*  
 Consiste em um dos seguintes:  
  
-   Um comando de consulta entre chaves (" {} ") que retorna um objeto de **conjunto de registros** filho. O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos desse provedor. Normalmente, essa será a linguagem SQL, embora o ADO não exija nenhuma linguagem de consulta específica.  
  
-   O nome de um conjunto de **registros**moldado existente.  
  
-   Outro comando de forma.  
  
-   A palavra-chave TABLE, seguida pelo nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias usado para fazer referência ao **conjunto de registros** retornado pelo *comando filho.* O *alias filho* é necessário na lista de colunas da cláusula COMPUTE e define a relação entre os objetos **Recordset** pai e filho.  
  
 *appended-column-list*  
 Uma lista na qual cada elemento define uma coluna no pai gerado. Cada elemento contém uma coluna de capítulo, uma nova coluna, uma coluna calculada ou um valor resultante de uma função de agregação no **conjunto de registros**filho.  
  
 *grp-field-list*  
 Uma lista de colunas nos objetos de conjunto de **registros** pai e filho que especifica como as linhas devem ser agrupadas no filho.  
  
 Para cada coluna na *lista GRP-Field-,* há uma coluna correspondente nos objetos do **conjunto de registros** filho e pai. Para cada linha no conjunto de **registros**pai, as colunas *GRP-field-list* têm valores exclusivos, e o **conjunto de registros** filho referenciado pela linha pai consiste exclusivamente em linhas filhas cujas colunas *GRP-field-list* têm os mesmos valores que a linha pai.  
  
 Se a cláusula BY for incluída, as linhas do **conjunto de registros**filho serão agrupadas com base nas colunas na cláusula COMPUTE. O **conjunto de registros** pai conterá uma linha para cada grupo de linhas no **conjunto de registros**filho.  
  
 Se a cláusula BY for omitida, o **conjunto de registros** filho inteiro será tratado como um único grupo e o **conjunto de registros** pai conterá exatamente uma linha. Essa linha fará referência a todo o **conjunto de registros**filho. Omitir a cláusula BY permite que você calcule agregações "total geral" em todo o **conjunto de registros**filho.  
  
 Por exemplo:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Independentemente da maneira como o **conjunto de registros** pai é formado (usando Compute ou usando append), ele conterá uma coluna de capítulo que é usada para relacioná-la a um **conjunto de registros**filho. Se desejar, o conjunto de **registros** pai também poderá conter colunas que contêm agregações (Sum, min, Max e assim por diante) nas linhas filhas. O **conjunto de registros** pai e filho pode conter colunas que contêm uma expressão na linha do conjunto de **registros**, bem como colunas novas e inicialmente vazias.  
  
## <a name="operation"></a>Operação  
 O *comando filho* é emitido para o provedor, que retorna um conjunto de **registros**filho.  
  
 A cláusula COMPUTE especifica as colunas do conjunto de **registros**pai, que pode ser uma referência ao **conjunto de registros**filho, uma ou mais agregações, uma expressão calculada ou novas colunas. Se houver uma cláusula BY, as colunas que ele definir também serão acrescentadas ao conjunto de **registros**pai. A cláusula BY especifica como as linhas do conjunto de **registros** filho são agrupadas.  
  
 Por exemplo, suponha que você tenha uma tabela, chamada demográficos, que consiste em campos de estado, cidade e população. (Os valores da população na tabela são fornecidos exclusivamente como um exemplo).  
  
|Estado|City|População|  
|-----------|----------|----------------|  
|WA|Seattle|700.000|  
|OU|Medford|200.000|  
|OU|Portland|400.000|  
|CA|Los Angeles|800.000|  
|CA|San Diego|600.000|  
|WA|Tacoma|500.000|  
|OU|Corvallis|300.000|  
  
 Agora, emita este comando de forma:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Esse comando abre um **conjunto de registros** moldado com dois níveis. O nível pai é um **conjunto de registros** gerado com uma coluna de agregação ( `SUM(rs.population)` ), uma coluna que faz referência ao **conjunto de registros** filho ( `rs` ) e uma coluna para agrupar o **conjunto de registros** filho ( `state` ). O nível filho é o **conjunto de registros** retornado pelo comando de consulta ( `select * from demographics` ).  
  
 As linhas de detalhes do **conjunto de registros** filho serão agrupadas por Estado, mas, caso contrário, em nenhuma ordem específica. Ou seja, os grupos não estarão em ordem alfabética ou numérica. Se desejar que o **conjunto de registros** pai seja ordenado, você poderá usar o método de classificação de **conjunto de registros** para ordenar o conjunto de **registros**pai.  
  
 Agora você pode navegar no conjunto de **registros** pai aberto e acessar os objetos do **conjunto de registros** de detalhes filho. Para obter mais informações, consulte [acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Conjuntos de registros de detalhes pai e filho resultante  
  
### <a name="parent"></a>Pai  
  
|SUM (RS. Média|rs|Estado|  
|---------------------------|--------|-----------|  
|1,3 milhões|Referência a child1|CA|  
|1,2 milhões|Referência a child2|WA|  
|1,1 milhões|Referência a child3|OU|  
  
## <a name="child1"></a>Filho1  
  
|Estado|City|População|  
|-----------|----------|----------------|  
|CA|Los Angeles|800.000|  
|CA|San Diego|600.000|  
  
## <a name="child2"></a>Filho2  
  
|Estado|City|População|  
|-----------|----------|----------------|  
|WA|Seattle|700.000|  
|WA|Tacoma|500.000|  
  
## <a name="child3"></a>Filho3  
  
|Estado|City|População|  
|-----------|----------|----------------|  
|OU|Medford|200.000|  
|OU|Portland|400.000|  
|OU|Corvallis|300.000|  
  
## <a name="see-also"></a>Consulte Também  
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral do data Shaping](../../../ado/guide/data/data-shaping-overview.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Objeto Recordset (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Provedores necessários para o Shaping de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula de ANEXAção de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Propriedade Value (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
