---
title: Cláusula de ANEXAção de forma | Microsoft Docs
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.custom: ''
ms.date: 01/19/2017
ms.reviewer: ''
ms.topic: conceptual
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
author: rothja
ms.author: jroth
ms.openlocfilehash: d26f83985ce74edc0581ff9ff8fee31d5064c7e5
ms.sourcegitcommit: 6037fb1f1a5ddd933017029eda5f5c281939100c
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/04/2020
ms.locfileid: "82760862"
---
# <a name="shape-append-clause"></a>Cláusula APPEND de forma
A cláusula comando de forma APPEND acrescenta uma coluna ou colunas a um **conjunto de registros**. Frequentemente, essas colunas são colunas de capítulo, que se referem a um **conjunto de registros**filho.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Descrição  
 As partes dessa cláusula são as seguintes:  
  
 *parent-command*  
 Zero ou um dos seguintes (você pode omitir completamente o *comando pai* ):  
  
-   Um comando de provedor entre chaves (" {} ") que retorna um objeto **Recordset** . O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos desse provedor. Normalmente, essa será a linguagem SQL, embora o ADO não exija nenhuma linguagem de consulta específica.  
  
-   Outro comando de forma inserido entre parênteses.  
  
-   A palavra-chave TABLE, seguida pelo nome de uma tabela no provedor de dados.  
  
 *parent-alias*  
 Um alias opcional que se refere ao **conjunto de registros**pai.  
  
 *lista de colunas*  
 Um ou mais dos seguintes:  
  
-   Uma coluna de agregação.  
  
-   Uma coluna calculada.  
  
-   Uma nova coluna criada usando a nova cláusula.  
  
-   Uma coluna de capítulo. Uma definição de coluna de capítulo é colocada entre parênteses ("()"). Consulte a sintaxe a seguir.  
  
```  
SHAPE [parent-command [[AS] parent-alias]]  
   APPEND (child-recordset [ [[AS] child-alias]   
      RELATE parent-column TO child-column | PARAMETER param-number, ... ])  
   [[AS] chapter-alias]   
   [, ... ]  
```  
  
## <a name="remarks"></a>Comentários  
 *child-recordset*  
 -   Um comando de provedor entre chaves (" {} ") que retorna um objeto **Recordset** . O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos desse provedor. Normalmente, essa será a linguagem SQL, embora o ADO não exija nenhuma linguagem de consulta específica.  
  
-   Outro comando de forma inserido entre parênteses.  
  
-   O nome de um conjunto de **registros**moldado existente.  
  
-   A palavra-chave TABLE, seguida pelo nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias que se refere ao **conjunto de registros**filho.  
  
 *parent-column*  
 Uma coluna no **conjunto de registros** retornada pelo *comando pai.*  
  
 *child-column*  
 Uma coluna no **conjunto de registros** retornada pelo *comando filho*.  
  
 *param-Number*  
 Consulte a [operação de comandos com parâmetros](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *chapter-alias*  
 Um alias que se refere à coluna de capítulo anexada ao pai.  
  
> [!NOTE]
>  A cláusula *"pai-coluna* para *filho-Column"* é, na verdade, uma lista, onde cada relação definida é separada por uma vírgula  
  
> [!NOTE]
>  A cláusula após a palavra-chave APPEND é, na verdade, uma lista, em que cada cláusula é separada por uma vírgula e define outra coluna a ser acrescentada ao pai.  
  
## <a name="remarks"></a>Comentários  
 Quando você constrói comandos de provedor da entrada do usuário como parte de um comando de forma, a forma tratará o comando de provedor fornecido pelo usuário como uma cadeia de caracteres opaca e os passará de maneira precisa para o provedor. Por exemplo, no comando de forma a seguir,  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 A forma executará dois comandos: `select * from t1` e ( `select * from t2 RELATE k1 TO k2)` . Se o usuário fornecer um comando composto que consiste em vários comandos de provedor separados por ponto e vírgula, a forma não será capaz de distinguir a diferença. Portanto, no comando de forma a seguir,  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 A forma `select * from t1; drop table t1` é executada e ( `select * from t2 RELATE k1 TO k2),` não percebendo que `drop table t1` é um comando de provedor separado e, nesse caso, perigoso. Os aplicativos sempre devem validar a entrada do usuário para evitar que tais ataques de hacker potenciais ocorram.  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Operação de comandos não parametrizados](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Operação de comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandos híbridos](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Cláusulas COMPUTE de forma de intervenção](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Exemplo de formatação de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
