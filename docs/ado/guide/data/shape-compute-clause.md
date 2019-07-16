---
title: Cláusula COMPUTE de forma | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: fa6862808643f3d687fa406cb3fc2aa23c9b7d7b
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67924141"
---
# <a name="shape-compute-clause"></a>Cláusula COMPUTE de forma
Uma cláusula COMPUTE de forma gera um pai **conjunto de registros**, cujas colunas consistem em uma referência para o filho **conjunto de registros**; opcional colunas cujo conteúdo é capítulo, novo, ou colunas calculadas, ou o resultado da execução de funções de agregação no filho **conjunto de registros** ou formatados anteriormente **conjunto de registros**; e todas as colunas de filho **Recordset** listados em o opcional pela cláusula.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE child-command [AS] child-alias  
   COMPUTE child-alias [[AS] name], [appended-column-list]  
   [BY grp-field-list]  
```  
  
## <a name="description"></a>Descrição  
 As partes dessa cláusula são da seguinte maneira:  
  
 *child-command*  
 Consiste em uma das seguintes opções:  
  
-   Um comando de consulta entre chaves ("{}") que retornará um filho **Recordset** objeto. O comando for emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não exige qualquer linguagem de consulta específica.  
  
-   O nome de um existente em forma **conjunto de registros**.  
  
-   Comando de outra forma.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias usado para fazer referência a **conjunto de registros** retornado pela *comando filho.* O *filho alias* é necessária na lista de colunas na cláusula COMPUTE e define a relação entre pai e filho **Recordset** objetos.  
  
 *appended-column-list*  
 Uma lista na qual cada elemento define uma coluna no pai gerado. Cada elemento contém uma coluna de capítulo, uma nova coluna, uma coluna calculada ou um valor resultante de uma função de agregação no filho **conjunto de registros**.  
  
 *grp-field-list*  
 Uma lista de colunas pai e filho **Recordset** objetos que especifica como as linhas devem ser agrupadas no filho.  
  
 Para cada coluna na *grp--lista de campos* há uma coluna correspondente no pai e filho **Recordset** objetos. Para cada linha no pai **conjunto de registros**, o *lista de campos grp* colunas têm valores exclusivos e o filho **Recordset** referenciado pelo pai linha consiste exclusivamente em filho linhas cuja *lista de campos grp* colunas têm os mesmos valores que a linha pai.  
  
 Se a cláusula BY for incluída, o filho **Recordset**do linhas serão agrupadas com base nas colunas na cláusula COMPUTE. O pai **conjunto de registros** conterá uma linha para cada grupo de linhas filho **conjunto de registros**.  
  
 Se a cláusula BY for omitida, o filho todo **conjunto de registros** é tratado como um único grupo e o pai **Recordset** irá conter exatamente uma linha. Essa linha fará referência a inteiro filho **conjunto de registros**. Omitir a cláusula BY permite computar agregações de "total geral" ao longo de todo filho **conjunto de registros**.  
  
 Por exemplo:  
  
```  
SHAPE {select * from Orders} AS orders             COMPUTE orders, SUM(orders.OrderAmount) as TotalSales         
```  
  
 Independentemente de qual modo o pai **conjunto de registros** é formado (usando a computação ou usando o ACRÉSCIMO), ele conterá uma coluna de capítulo que é usada para relacioná-la a um filho **conjunto de registros**. Se desejar, o pai **Recordset** também podem conter colunas que contêm agregações (SUM, MIN, MAX e assim por diante) em relação às linhas filho. O pai e filho **conjunto de registros** podem conter colunas que contêm uma expressão na linha a **conjunto de registros**, bem como as colunas que são novos e inicialmente vazio.  
  
## <a name="operation"></a>Operação  
 O *filho-command* é emitido para o provedor, que retorna um filho **conjunto de registros**.  
  
 A cláusula COMPUTE Especifica as colunas do pai **conjunto de registros**, que pode ser uma referência para o filho **conjunto de registros**, uma ou mais agregações, uma expressão calculada ou novas colunas. Se houver uma cláusula BY, as colunas que ele define também são acrescentadas ao pai **conjunto de registros**. A cláusula BY Especifica como as linhas do filho **Recordset** são agrupados.  
  
 Por exemplo, suponha que você tenha uma tabela denominada dados demográficos, que consiste em campos de estado, cidade e população. (As figuras de população da tabela são fornecidas somente como um exemplo).  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|WA|Seattle|700,000|  
|OU|Medford|200,000|  
|OU|Portland|400,000|  
|CA|Los Angeles|800,000|  
|CA|SAN Diego|600,000|  
|WA|Tacoma|500,000|  
|OU|Corvallis|300,000|  
  
 Agora, execute este comando de forma:  
  
```  
rst.Open  "SHAPE {select * from demographics} AS rs "  & _  
          "COMPUTE rs, SUM(rs.population) BY state", _  
           objConnection  
```  
  
 Esse comando abre uma moldado **Recordset** com dois níveis. O nível pai é uma gerada **conjunto de registros** com uma coluna de agregação (`SUM(rs.population)`), uma coluna referenciando o filho **conjunto de registros** (`rs`) e uma coluna para agrupar o filho **Recordset** (`state`). O nível filho é o **conjunto de registros** retornada pelo comando de consulta (`select * from demographics`).  
  
 O filho **Recordset** linhas de detalhes serão agrupados por estado, mas caso contrário, sem nenhuma ordem específica. Ou seja, não serão os grupos em ordem alfabética ou numérica. Se você quiser que o pai **conjunto de registros** para serem ordenados, você pode usar o **classificação do conjunto de registros** método para fazer o pedido pai **conjunto de registros**.  
  
 Agora, você pode navegar pai aberto **conjunto de registros** e acessar os detalhes de filho **Recordset** objetos. Para obter mais informações, consulte [acessar linhas em um conjunto de registros hierárquicos](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md).  
  
## <a name="resultant-parent-and-child-detail-recordsets"></a>Pai resultante e conjuntos de registros de detalhe de filho  
  
### <a name="parent"></a>Pai  
  
|Soma (rs. População)|rs|Estado|  
|---------------------------|--------|-----------|  
|1,300,000|Referência ao child1|CA|  
|1,200,000|Referência a child2|WA|  
|1,100,000|Referência a child3|OU|  
  
## <a name="child1"></a>Child1  
  
|Estado|Cidade|População|  
|-----------|----------|----------------|  
|CA|Los Angeles|800,000|  
|CA|SAN Diego|600,000|  
  
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
 [Acessando linhas em um conjunto de registros hierárquico](../../../ado/guide/data/accessing-rows-in-a-hierarchical-recordset.md)   
 [Visão geral de modelagem de dados](../../../ado/guide/data/data-shaping-overview.md)   
 [Objeto Field](../../../ado/reference/ado-api/field-object.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Objeto de conjunto de registros (ADO)](../../../ado/reference/ado-api/recordset-object-ado.md)   
 [Provedores necessários para Data Shaping](../../../ado/guide/data/required-providers-for-data-shaping.md)   
 [Cláusula APPEND de forma](../../../ado/guide/data/shape-append-clause.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)   
 [Propriedade Value (ADO)](../../../ado/reference/ado-api/value-property-ado.md)   
 [Funções do Visual Basic for Applications](../../../ado/guide/data/visual-basic-for-applications-functions.md)
