---
title: Parâmetros de declaração | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 02327ff4bb6a1ac3ac57fbf7d3c6b09b70c11534
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306817"
---
# <a name="statement-parameters"></a>Parâmetros de instrução
Um *parâmetro* é uma variável em uma declaração SQL. Por exemplo, suponha que uma tabela De peças tenha colunas chamadas PartID, Description e Price. Adicionar uma peça sem parâmetros exigiria a construção de uma declaração SQL, como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Embora esta instrução insira uma nova ordem, não é uma boa solução para um aplicativo de entrada de pedidos porque os valores a serem inseridos não podem ser codificados no aplicativo. Uma alternativa é construir a instrução SQL em tempo de execução, utilizando os valores a serem inseridos. Esta também não é uma boa solução, devido à complexidade da construção de declarações em tempo de execução. A melhor solução é substituir os elementos da cláusula **VALUES** por pontos de interrogação (?), ou *marcadores de parâmetro:*  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Os marcadores de parâmetro são associados a variáveis do aplicativo. Para adicionar uma nova linha, o aplicativo tem apenas que definir os valores das variáveis e executar a declaração. O driver recupera os valores atuais das variáveis e os envia para a fonte de dados. Se a declaração for executada várias vezes, o aplicativo poderá tornar o processo ainda mais eficiente, preparando a declaração.  
  
 A instrução mostrada pode ser codificada em um aplicativo de entrada de pedidos para inserir uma nova linha. No entanto, os marcadores de parâmetros não se limitam a aplicações verticais. Para qualquer aplicação, eles facilitam a dificuldade de construir instruções SQL no tempo de execução, evitando conversões de e para texto. Por exemplo, a parte iD mostrada é provavelmente armazenada no aplicativo como um inteiro. Se a declaração SQL for construída sem marcadores de parâmetros, o aplicativo deve converter a parte ID em texto e a fonte de dados deve convertê-la de volta a um inteiro. Usando um marcador de parâmetro, o aplicativo pode enviar o ID de peça para o driver como um inteiro, que geralmente pode enviá-lo para a fonte de dados como um inteiro. Isso salva duas conversões. Para valores de dados longos, isso é muito importante, porque as formas de texto de tais valores frequentemente excedem o comprimento permitido de uma declaração SQL.  
  
 Os parâmetros são válidos apenas em determinados lugares em instruções SQL. Por exemplo, eles não são permitidos na lista de seleção (a lista de colunas a ser devolvida por uma declaração **SELECT),** nem são permitidas como ambos os operands de um operador binário, como o sinal igual (=), porque seria impossível determinar o tipo de parâmetro. Geralmente, os parâmetros são válidos apenas em instruções DML (Data Manipulation Language, linguagem de manipulação de dados) e não em instruções DDL (Data Definition Language, linguagem de definição de dados). Para obter mais informações, consulte [Marcadores de parâmetros](../../../odbc/reference/appendixes/parameter-markers.md) no apêndice C: Gramática SQL.  
  
 Quando a declaração SQL invoca um procedimento, os parâmetros nomeados podem ser usados. Os parâmetros nomeados são identificados por seus nomes, não por sua posição na declaração SQL. Eles podem ser vinculados por uma chamada ao **SQLBindParameter,** mas o parâmetro é identificado pelo campo SQL_DESC_NAME do IPD (descritor de parâmetro de implementação), não pelo argumento *ParameterNumber* do **SQLBindParameter**. Eles também podem ser vinculados chamando **SQLSetDescField** ou **SQLSetDescRec**. Para obter mais informações sobre os parâmetros nomeados, consulte [Parâmetros de vinculação por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), mais tarde nesta seção. Para obter mais informações sobre descritores, consulte [Descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associando parâmetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurar valores de parâmetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviar dados Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperando parâmetros de saída por SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parâmetros de procedimento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matriz de valores de parâmetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
