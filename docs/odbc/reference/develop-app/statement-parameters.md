---
title: Parâmetros de instrução | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- statement parameters [ODBC]
ms.assetid: 58d5b166-2578-4699-a560-1f1e6d86c49a
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: e2b9e21fe7bb4252149b7b6ef5cbb334756821f5
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="statement-parameters"></a>Parâmetros de instrução
Um *parâmetro* é uma variável em uma instrução SQL. Por exemplo, suponha que uma tabela de peças possui colunas nomeadas PartID, descrição e preço. Para adicionar uma parte sem parâmetros exigiria construindo uma instrução SQL, como:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (2100, 'Drive shaft', 50.00)  
```  
  
 Embora essa instrução insere um novo pedido, ele não é uma boa solução para um aplicativo de entrada de ordem porque os valores para inserir não podem ser embutida em código no aplicativo. Uma alternativa é criar a instrução SQL em tempo de execução usando os valores a serem inseridos. Isso também não é uma boa solução, devido à complexidade das instruções de criação em tempo de execução. A melhor solução é substituir os elementos do **valores** cláusula com pontos de interrogação (?), ou *marcadores de parâmetro*:  
  
```  
INSERT INTO Parts (PartID, Description, Price) VALUES (?, ?, ?)  
```  
  
 Os marcadores de parâmetro são associados a variáveis do aplicativo. Para adicionar uma nova linha, o aplicativo precisa apenas definir os valores das variáveis e execute a instrução. O driver recupera os valores atuais das variáveis e os envia para a fonte de dados. Se a instrução for executada várias vezes, o aplicativo pode tornar o processo ainda mais eficiente, preparando a instrução.  
  
 A instrução mostrada apenas pode ser embutida em um aplicativo de entrada de ordem para inserir uma nova linha. No entanto, os marcadores de parâmetro não estão limitados para aplicativos verticais. Para qualquer aplicativo, eles facilitam a dificuldade de construindo instruções SQL em tempo de execução, evitando conversões para e de texto. Por exemplo, a ID de parte mostrada apenas é mais provável armazenados no aplicativo como um inteiro. Se a instrução SQL é construída sem marcadores de parâmetro, o aplicativo deve converter o ID da parte em texto e a fonte de dados deve convertê-lo novamente como um número inteiro. Usando um marcador de parâmetro, o aplicativo pode enviar a ID de parte do driver como um inteiro, que geralmente pode enviá-lo à fonte de dados como um número inteiro. Isso economiza duas conversões. Para valores de dados longos, isso é muito importante, porque as formas de texto de valores tão frequentemente excederem o comprimento permitido de uma instrução SQL.  
  
 Parâmetros são válidos somente em certos locais nas instruções SQL. Por exemplo, eles não são permitidos na lista de seleção (lista de colunas a serem retornadas por uma **selecione** instrução), nem eles são permitidos como ambos os operandos de um operador binário, como o sinal de igual (=), pois ele seria impossível Determine o tipo de parâmetro. Em geral, os parâmetros são válidos apenas nas instruções de linguagem de manipulação de dados (DML) e não em instruções de linguagem de definição de dados (DDL). Para obter mais informações, consulte [marcadores de parâmetro](../../../odbc/reference/appendixes/parameter-markers.md) na gramática do apêndice c: SQL.  
  
 Quando a instrução SQL chama um procedimento, parâmetros nomeado pode ser usado. Parâmetros nomeados são identificados por seus nomes, não com sua posição na instrução SQL. Eles podem ser vinculados por uma chamada para **SQLBindParameter**, mas o parâmetro é identificado pelo campo SQL_DESC_NAME do IPD (descritor de parâmetro de implementação), não pelo *ParameterNumber* argumento de **SQLBindParameter**. Eles também podem ser associados chamando **SQLSetDescField** ou **SQLSetDescRec**. Para obter mais informações sobre parâmetros nomeados, consulte [associando parâmetros por nome (parâmetros nomeados)](../../../odbc/reference/develop-app/binding-parameters-by-name-named-parameters.md), mais adiante nesta seção. Para obter mais informações sobre descritores, consulte [descritores](../../../odbc/reference/develop-app/descriptors.md).  
  
 Esta seção contém os tópicos a seguir.  
  
-   [Parâmetros de associação](../../../odbc/reference/develop-app/binding-parameters-odbc.md)  
  
-   [Configurando valores de parâmetro](../../../odbc/reference/develop-app/setting-parameter-values.md)  
  
-   [Enviando dados Long](../../../odbc/reference/develop-app/sending-long-data.md)  
  
-   [Recuperando parâmetros de saída por SQLGetData](../../../odbc/reference/develop-app/retrieving-output-parameters-using-sqlgetdata.md)  
  
-   [Parâmetros de procedimento](../../../odbc/reference/develop-app/procedure-parameters.md)  
  
-   [Matriz de valores de parâmetros](../../../odbc/reference/develop-app/arrays-of-parameter-values.md)
