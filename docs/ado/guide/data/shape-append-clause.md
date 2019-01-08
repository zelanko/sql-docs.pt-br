---
title: Cláusula APPEND de forma | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 13a91d6b8512b2c1287c3cc8e36e43a1317022d7
ms.sourcegitcommit: 6443f9a281904af93f0f5b78760b1c68901b7b8d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/11/2018
ms.locfileid: "53208484"
---
# <a name="shape-append-clause"></a>Cláusula APPEND de forma
A cláusula de ACRÉSCIMO do comando de forma acrescenta uma coluna ou colunas para um **conjunto de registros**. Com frequência, essas colunas são colunas de capítulo que se referem a um filho **conjunto de registros**.  
  
## <a name="syntax"></a>Sintaxe  
  
```  
SHAPE [parent-command [[AS] parent-alias]] APPEND column-list  
```  
  
## <a name="description"></a>Descrição  
 As partes dessa cláusula são da seguinte maneira:  
  
 *parent-command*  
 Zero ou uma das opções a seguir (você pode omitir as *comando pai* completamente):  
  
-   Um comando de provedor entre chaves ("{}") que retorna um **Recordset** objeto. O comando for emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não exige qualquer linguagem de consulta específica.  
  
-   Inserido comando de outra forma entre parênteses.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *parent-alias*  
 Um alias opcional que se refere ao pai **conjunto de registros**.  
  
 *column-list*  
 Um ou mais das seguintes opções:  
  
-   Uma coluna agregada.  
  
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
 -   Um comando de provedor entre chaves ("{}") que retorna um **Recordset** objeto. O comando for emitido para o provedor de dados subjacente e sua sintaxe depende dos requisitos do provedor. Isso geralmente será a linguagem SQL, embora o ADO não exige qualquer linguagem de consulta específica.  
  
-   Inserido comando de outra forma entre parênteses.  
  
-   O nome de um existente em forma **conjunto de registros**.  
  
-   A tabela a palavra-chave, seguida do nome de uma tabela no provedor de dados.  
  
 *child-alias*  
 Um alias que se refere ao filho **conjunto de registros**.  
  
 *parent-column*  
 Uma coluna na **conjunto de registros** retornado pela *comando pai.*  
  
 *child-column*  
 Uma coluna na **conjunto de registros** retornado pela *comando filho*.  
  
 *param-number*  
 Ver [operação de comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md).  
  
 *chapter-alias*  
 Um alias que refere-se para a coluna de capítulo anexada ao pai.  
  
> [!NOTE]
>  O *"coluna pai* TO *coluna filho"* cláusula é, na verdade, uma lista, onde cada relação definida é separada por uma vírgula  
  
> [!NOTE]
>  A cláusula após a palavra-chave de ACRÉSCIMO é, na verdade, uma lista, onde cada cláusula é separada por uma vírgula e define a outra coluna a ser acrescentado ao pai.  
  
## <a name="remarks"></a>Comentários  
 Quando você constrói os comandos do provedor da entrada do usuário como parte de um comando de forma, forma tratará o fornecido pelo usuário um comando do provedor como uma cadeia de caracteres opaca e passá-los fielmente ao provedor. Por exemplo, no comando de forma a seguir,  
  
```  
SHAPE {select * from t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 FORMA irá executar dois comandos: `select * from t1` e (`select * from t2 RELATE k1 TO k2)`. Se o usuário fornece um comando composto que consiste em vários comandos de provedor, separados por ponto e vírgula, forma não é capaz de distinguir a diferença. Portanto, o seguinte comando de forma  
  
```  
SHAPE {select * from t1; drop table t1} APPEND ({select * from t2} RELATE k1 TO k2)  
```  
  
 Executa de forma `select * from t1; drop table t1` e (`select * from t2 RELATE k1 TO k2),` sem perceber que `drop table t1` é uma separado e neste comando perigoso, caso, o provedor. Aplicativos sempre devem validar o entrada do usuário para impedir esses ataques potenciais do hacker.  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Operação de comandos não parametrizados](../../../ado/guide/data/operation-of-non-parameterized-commands.md)  
  
-   [Operação de comandos parametrizados](../../../ado/guide/data/operation-of-parameterized-commands.md)  
  
-   [Comandos híbridos](../../../ado/guide/data/hybrid-commands.md)  
  
-   [Cláusulas COMPUTE de forma de intervenção](../../../ado/guide/data/intervening-shape-compute-clauses.md)  
  
## <a name="see-also"></a>Consulte também  
 [Exemplo de Data Shaping](../../../ado/guide/data/data-shaping-example.md)   
 [Gramática de forma formal](../../../ado/guide/data/formal-shape-grammar.md)   
 [Modelar comandos em geral](../../../ado/guide/data/shape-commands-in-general.md)
