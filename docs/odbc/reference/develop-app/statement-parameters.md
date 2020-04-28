---
title: Parâmetros da instrução | Microsoft Docs
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
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81306817"
---
# <a name="statement-parameters"></a>Parâmetros de instrução
Um *parâmetro* é uma variável em uma instrução SQL. Por exemplo, suponha que uma tabela de peças tenha colunas denominadas partid, descrição e preço. Para adicionar uma parte sem parâmetros, seria necessário construir uma instrução SQL, como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Embora essa instrução Insira um novo pedido, ela não é uma boa solução para um aplicativo de entrada de pedidos porque os valores a serem inseridos não podem ser embutidos em código no aplicativo. Uma alternativa é construir a instrução SQL em tempo de execução, usando os valores a serem inseridos. Essa também não é uma boa solução, devido à complexidade da construção de instruções em tempo de execução. A melhor solução é substituir os elementos da cláusula **Values** por pontos de interrogação (?) ou *marcadores de parâmetro*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Os marcadores de parâmetro são associados a variáveis do aplicativo. Para adicionar uma nova linha, o aplicativo tem apenas que definir os valores das variáveis e executar a instrução. O driver recupera os valores atuais das variáveis e os envia para a fonte de dados. Se a instrução for executada várias vezes, o aplicativo poderá tornar o processo ainda mais eficiente, preparando a instrução.  
  
 A instrução que acaba de ser mostrada pode ser embutida em código em um aplicativo de entrada de pedido para inserir uma nova linha. No entanto, os marcadores de parâmetro não estão limitados a aplicativos verticais. Para qualquer aplicativo, eles facilitam a dificuldade de construir instruções SQL em tempo de execução, evitando conversões de e para texto. Por exemplo, a ID da parte que acaba de ser mostrada é provavelmente armazenada no aplicativo como um inteiro. Se a instrução SQL for construída sem marcadores de parâmetro, o aplicativo deverá converter a ID de parte em texto e a fonte de dados deverá convertê-la de volta em um inteiro. Usando um marcador de parâmetro, o aplicativo pode enviar a ID da parte para o driver como um inteiro, que geralmente pode enviá-la para a fonte de dados como um inteiro. Isso salva duas conversões. Para valores de dados longos, isso é muito importante, pois as formas de texto desses valores geralmente excedem o comprimento permitido de uma instrução SQL.  
  
 Os parâmetros são válidos somente em determinados locais nas instruções SQL. Por exemplo, eles não são permitidos na lista de seleção (a lista de colunas a serem retornadas por uma instrução **Select** ), nem são permitidas como ambos os operandos de um operador binário, como o sinal de igual (=), porque seria impossível determinar o tipo de parâmetro. Em geral, os parâmetros são válidos somente em instruções DML (linguagem de manipulação de dados) e não em instruções DDL (linguagem de definição de dados). Para obter mais informações, consulte [marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md) no Apêndice C: gramática SQL.  
  
 Quando a instrução SQL invoca um procedimento, parâmetros nomeados podem ser usados. Os parâmetros nomeados são identificados por seus nomes, não pela sua posição na instrução SQL. Eles podem ser associados a uma chamada para **SQLBindParameter**, mas o parâmetro é identificado pelo campo SQL_DESC_NAME do IPD (descritor de parâmetro de implementação), não pelo argumento *ParameterNumber* de **SQLBindParameter**. Eles também podem ser associados chamando **SQLSetDescField** ou **SQLSetDescRec**. Para obter mais informações sobre parâmetros nomeados, consulte [ligando parâmetros por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), mais adiante nesta seção. Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta seção contém os seguintes tópicos.  
  
-   [Associando parâmetros](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurar valores de parâmetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviar dados Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperando parâmetros de saída por SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parâmetros de procedimento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matriz de valores de parâmetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
