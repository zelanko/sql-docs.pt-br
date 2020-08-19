---
description: Mapeamento SQLSetConnectOption
title: Mapeamento de SQLSetConnectOption | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 6c1f1379bfd2bbc2faccf719d68009ed63b350fd
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476958"
---
# <a name="sqlsetconnectoption-mapping"></a>Mapeamento SQLSetConnectOption
Quando um ODBC 2. *x* o aplicativo chama **SQLSetConnectOption** por meio de um driver ODBC 3 *. x* , a chamada para  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 o resultado será o seguinte:  
  
-   Se *fOption* indicar um atributo de conexão definido pelo ODBC que requer uma cadeia de caracteres, o Gerenciador de driver chamará  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indicar um atributo de conexão definido pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver chamará  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indicar um atributo de conexão definido por Driver, o Gerenciador de driver chamará  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o argumento *ConnectionHandle* é definido como o valor em *HDBC*, o argumento de *atributo* é definido como o valor em *fOption*e o argumento *ValuePtr* é definido com o mesmo valor de *vParam*.  
  
 Como o Gerenciador de driver não sabe se o atributo de conexão definido pelo driver precisa de um valor inteiro de cadeia de caracteres ou de 32 bits, ele precisa passar um valor válido para o argumento *BufferLength* de **SQLSetConnectAttr**. Se o driver tiver definido semântica especial para atributos de conexão definidos pelo driver e precisar ser chamado usando **SQLSetConnectOption**, ele deverá dar suporte a **SQLSetConnectOption**.  
  
 Se um ODBC 2. *x* Application chama **SQLSetConnectOption** para definir uma opção de instrução específica do driver em um driver ODBC 3 *. x* e a opção foi definida em um ODBC 2. versão *x* do driver, uma nova constante de manifesto deve ser definida para a opção no driver ODBC 3 *. x* . Se a constante de manifesto antiga for usada na chamada para **SQLSetConnectOption**, o Gerenciador de driver chamará **SQLSetConnectAttr** com o argumento **StringLength** definido como 0.  
  
 Para um driver ODBC 3 *. x* , o Gerenciador de driver não verifica mais se *fOption* está entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Definindo opções de instrução no nível de conexão  
 No ODBC 2. *x*, um aplicativo poderia chamar **SQLSetConnectOption** para definir uma opção de instrução. Quando isso é feito, o driver estabelece a opção de instrução como um padrão para qualquer instrução posteriormente alocada para essa conexão. Ele é definido por driver se o driver define a opção de instrução para quaisquer instruções existentes associadas à conexão especificada.  
  
 Essa capacidade foi preterida no ODBC 3 *. x*. Os drivers ODBC 3 *. x* precisam apenas de suporte para a configuração ODBC 2. atributos de instrução *x* no nível de conexão se desejarem trabalhar com ODBC 2. *x* aplicativos que fazem isso. Os aplicativos ODBC 3 *. x* nunca devem definir atributos de instrução no nível de conexão. Os atributos de instrução ODBC 3 *. x* não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e de instrução, e podem ser definidos no nível de conexão ou no nível de instrução.
