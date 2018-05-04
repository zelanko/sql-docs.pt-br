---
title: Mapeamento de SQLSetConnectOption | Microsoft Docs
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
- SQLSetConnectOption function [ODBC], mapping
- mapping deprecated functions [ODBC], SQLSetConnectOption
ms.assetid: a1b325cf-0c42-41c1-b141-b5a4fee7e708
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 255e59c3c9da81dfcc8dba13be46fc902e7a81b2
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="sqlsetconnectoption-mapping"></a>Mapeamento de SQLSetConnectOption
Quando um ODBC 2. *x* aplicativo chama **SQLSetConnectOption** por meio de um ODBC 3 *. x* driver, a chamada para  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 resulta da seguinte maneira:  
  
-   Se *fOption* indica um atributo de conexão definidas pelo ODBC que requer uma cadeia de caracteres, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indica um atributo de conexão definidas pelo ODBC que retorna um valor inteiro de 32 bits, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indica um atributo de conexão definidos pelo driver, as chamadas de Gerenciador de Driver  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o *identificador da conexão* argumento é definido como o valor em *hdbc*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o mesmo valor como *vParam*.  
  
 Porque o Gerenciador de Driver não sabe se o atributo de conexão definidos pelo driver precisa de uma cadeia de caracteres ou um valor inteiro de 32 bits, ele deve passar um valor válido para o *BufferLength* argumento de **SQLSetConnectAttr**. Se o driver definiu semântica especial para definidos pelo driver conectar atributos e precisa ser chamado usando **SQLSetConnectOption**, deverá dar suporte a **SQLSetConnectOption**.  
  
 Se um ODBC 2. *x* aplicativo chama **SQLSetConnectOption** para definir uma opção de instrução específicos de driver em um ODBC 3 *. x* driver e a opção foi definida em um ODBC 2. *x* a versão do driver, uma nova constante de manifesto deve ser definida para a opção ODBC 3 *. x* driver. Se a constante de manifesto antiga é usada na chamada para **SQLSetConnectOption**, o Gerenciador de Driver chamará **SQLSetConnectAttr** com o **StringLength** argumento definido como 0.  
  
 Para um ODBC 3 *. x* driver, o Gerenciador de Driver não verifica se *fOption* é entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX ou é maior do que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Definir opções de instrução em nível de Conexão  
 No ODBC 2. *x*, um aplicativo pode chamar **SQLSetConnectOption** para definir uma opção de instrução. Quando isso for feito, o driver estabelece a opção de instrução como padrão para todas as instruções posteriormente alocadas para essa conexão. Ele é definido pelo driver se o driver define a opção de instrução para qualquer instrução existente associado com a conexão especificada.  
  
 Essa capacidade foi preterida no ODBC 3 *. x*. ODBC 3 *. x* drivers precisam apenas oferece suporte à definição do ODBC 2. *x* atributos de instrução em nível de conexão se desejar trabalhar com ODBC 2. *x* aplicativos que fazem isso. ODBC 3 *. x* aplicativos nunca devem definir atributos de instrução no nível de conexão. ODBC 3 *. x* atributos de instrução não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e pode ser definir o nível de conexão ou o nível de instrução.
