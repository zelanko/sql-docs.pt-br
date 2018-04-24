---
title: Formatar a cláusula COMPUTE | Microsoft Docs
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: ado
ms.technology:
- drivers
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.suite: sql
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- compute clause [ADO]
- data shaping [ADO], COMPUTE clause
ms.assetid: 3fdfead2-b5ab-4163-9b1d-3d2143a5db8c
caps.latest.revision: 11
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 5a157d7d77bd6beefae7c3258039953c5e5e4995
ms.sourcegitcommit: bb044a48a6af9b9d8edb178dc8c8bd5658b9ff68
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2018
---
# <a name="shape-compute-clause"></a>Cláusula COMPUTE de forma
Uma cláusula COMPUTE de forma gera um pai **registros**, cujas colunas consistem em uma referência para o filho **registros**; opcional colunas cujo conteúdo é capítulo, novo, ou colunas calculadas, ou o resultado da execução de funções de agregação no filho **Recordset** ou de forma anteriormente **Recordset**; e todas as colunas de filho **Recordset** listados em opcional pela cláusula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Description  
 As partes dessa cláusula são da seguinte maneira:  
  
 *child-command*  
 Consiste em uma das seguintes opções:  
  
-   Um comando de consulta dentro de chaves ("{}") que retornará um filho **registros** objeto. O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não requer qualquer linguagem de consulta específica.  
  
-   O nome de um objeto existente em forma de **registros**.  
  
-   Comando de outra forma.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias usado para se referir a **registros** retornado pelo *comando filho.* O *filho alias* é necessária na lista de colunas na cláusula COMPUTE e define a relação entre pai e filho **registros** objetos.  
  
 *appended-column-list*  
 Uma lista na qual cada elemento define uma coluna no pai gerado. Cada elemento contém uma coluna de capítulo, uma nova coluna, uma coluna calculada ou um valor resultante de uma função de agregação no filho **registros**.  
  
 *grp-field-list*  
 Uma lista de colunas pai e filho **registros** objetos que especifica como as linhas devem ser agrupadas no filho.  
  
 Para cada coluna a *grp--lista de campos,* uma coluna correspondente no pai e filho **registros** objetos. Para cada linha no pai **registros**, o *grp lista de campos* colunas têm valores exclusivos e o filho **registros** referenciado pelo pai linha consiste exclusivamente filho linhas cuja *lista de campos grp* colunas têm os mesmos valores da linha pai.  
  
 Se a cláusula BY for incluída, o filho **registros**do linhas serão agrupadas com base nas colunas na cláusula COMPUTE. O pai **registros** conterá uma linha para cada grupo de linhas filho **registros**.  
  
 Se a cláusula BY for omitida, o filho todo **registros** é tratado como um único grupo e o pai **Recordset** irá conter exatamente uma linha. Essa linha fará referência filho todo **registros**. Omitir a cláusula BY permite computar agregações de "total geral" em todo filho **registros**.  
  
 Por exemplo:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Independentemente da maneira como o pai **registros** é formado (usando computação ou usando APPEND), ele conterá uma coluna de capítulo que é usada para relacioná-la a um filho **registros**. Se desejar, o pai **registros** também pode conter colunas que contêm agregações (SUM, MIN, MAX e assim por diante) sobre as linhas filho. O pai e filho **registros** pode conter colunas que contêm uma expressão na linha a **Recordset**, bem como colunas que são novos e inicialmente vazio.  
  
## <a name="operation"></a>Operação  
 O *filho comando* é emitido para o provedor, que retornará um filho **registros**.  
  
 A cláusula COMPUTE Especifica as colunas do pai **registros**, que pode ser uma referência para o filho **registros**, uma ou mais agregações, uma expressão calculada ou novas colunas. Se houver uma cláusula BY, as colunas que ele define também são acrescentadas ao pai **registros**. A cláusula BY Especifica como as linhas do filho **registros** são agrupados.  
  
 Por exemplo, suponha que você tenha uma tabela denominada dados demográficos, que consiste em campos de população de estado e cidade. (Os valores de população da tabela são fornecidos apenas como um exemplo).  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|OU|Medford|200,000|  
|OU|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|São Paulo|600,000|  
|WA|Tacoma|500,000|  
|OU|Corvallis|300,000|  
  
 Agora, execute este comando de forma:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Esse comando abre uma forma **registros** com dois níveis. O nível pai é uma gerada **registros** com uma coluna de agregação (`SUM(rs.population)`), uma coluna de referência filho **registros** (`rs`) e uma coluna para agrupar o filho **Registros** (`state`). O nível filho é o **registros** retornada pelo comando de consulta (`select * from demographics`).  
  
 O filho **registros** linhas de detalhes serão agrupados por estado, mas em nenhuma ordem específica. Ou seja, os grupos não será em ordem alfabética ou numérica. Se você quiser que o pai **registros** para ser ordenado, você pode usar o **classificação do conjunto de registros** método ordenar pai **registros**.  
  
 Agora você pode navegar pai aberto **registros** e acessar os detalhes de filho **registros** objetos. Para obter mais informações, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Pai resultante e conjuntos de registros de detalhe de filho  
  
### <a name="parent"></a>Pai  
  
|SUM (rs. População)|rs|Estado|  
|---------------------------|--------|-----------|  
|1,300,000|Referência a child1|CA|  
|1,200,000|Referência a child2|WA|  
|1,100,000|Referência a child3|OU|  
  
## <a name="child1"></a>Child1  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|São Paulo|600,000|  
  
## <a name="child2"></a>Child2  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|WA|Tacoma|500,000|  
  
## <a name="child3"></a>Child3  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|OU|Medford|200,000|  
|OU|Portland|400,000|  
|OU|Corvallis|300,000|  
  
## <a name="see-also"></a>Consulte também  
 [Acessar linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Provedores necessários para modelagem de dados](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Comandos de forma em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Propriedade de valor (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
