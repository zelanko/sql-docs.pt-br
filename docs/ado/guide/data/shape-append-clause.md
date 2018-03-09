---
title: "A forma de cláusula APPEND | Microsoft Docs"
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: ado
ms.technology:
- drivers
ms.custom: 
ms.date: 01/19/2017
ms.reviewer: 
ms.suite: sql
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- shape commands [ADO]
- data shaping [ADO], APPEND clause
- append clause [ADO]
ms.assetid: f90fcf55-6b24-401d-94e1-d65bd24bd342
caps.latest.revision: 
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8f4c9bf19fd1df07bb4271a8db94311548a4e092
ms.sourcegitcommit: acab4bcab1385d645fafe2925130f102e114f122
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/09/2018
---
# <a name="shape-append-clause"></a>Cláusula APPEND de forma
A cláusula de ACRÉSCIMO de comando de forma acrescenta uma coluna ou colunas para um **registros**. Com frequência, essas colunas são colunas de capítulo, o que fazer referência a um filho **registros**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Description  
 As partes dessa cláusula são da seguinte maneira:  
  
 *parent-command*  
 Zero ou um dos seguintes (você pode omitir o *comando pai* completamente):  
  
-   Um comando de provedor entre chaves ("{") que retorna um **registros** objeto. O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não requer qualquer linguagem de consulta específica.  
  
-   Inserido comando de outra forma entre parênteses.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *parent-alias*  
 Um alias opcional que se refere ao pai **registros**.  
  
 *column-list*  
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
  
## <a name="remarks"></a>Remarks  
 *child-recordset*  
 -   Um comando de provedor entre chaves ("{") que retorna um **registros** objeto. O comando é emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não requer qualquer linguagem de consulta específica.  
  
-   Inserido comando de outra forma entre parênteses.  
  
-   O nome de um objeto existente em forma de **registros**.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias que se refere ao filho **registros**.  
  
 *parent-column*  
 Uma coluna no **registros** retornado pelo *comando pai.*  
  
 *child-column*  
 Uma coluna no **registros** retornado pelo *filho comando*.  
  
 *param-number*  
 Consulte [operação de comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *chapter-alias*  
 Um alias que se refere à coluna de capítulo acrescentada ao pai.  
  
> [!NOTE]
>  O *"coluna pai* para *coluna filho"* cláusula é realmente uma lista, onde cada relação definida é separada por vírgula  
  
> [!NOTE]
>  A cláusula após a palavra-chave de ACRÉSCIMO é realmente uma lista, onde cada cláusula é separada por uma vírgula e define a outra coluna a ser acrescentada ao pai.  
  
## <a name="remarks"></a>Remarks  
 Quando você construir comandos do provedor da entrada do usuário como parte de um comando de forma, a forma tratar o usuário forneceu um comando de provedor como uma cadeia de caracteres opaca e passá-las precisamente para o provedor. Por exemplo, no comando de forma a seguir,  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 FORMA irá executar dois comandos: `select * from t1` e (`select * from t2 RELATE k1 TO k2)`. Se o usuário fornece um comando composto que consiste em vários comandos de provedor, separados por ponto e vírgula, forma não é capaz de distinguir a diferença. Isso o seguinte comando de forma  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Executa de forma `select * from t1; drop table t1` e (`select * from t2 RELATE k1 TO k2),` não perceber que `drop table t1` é uma separado e nesse comando perigoso, caso, o provedor. Aplicativos sempre devem validar o entrada do usuário para impedir a ocorrência de tais ataques de hacker.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Operação de comandos não parametrizados](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Operação de comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandos híbridos](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Cláusulas COMPUTE de forma de intervenção](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de modelagem de dados](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
