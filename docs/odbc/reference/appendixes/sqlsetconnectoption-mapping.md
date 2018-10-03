---
title: Mapeamento SQLSetConnectOption | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0351a6fa4621acb09d18a72b32ec2010a605ed9b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47769564"
---
# <a name="sqlsetconnectoption-mapping"></a>Mapeamento SQLSetConnectOption
Quando um ODBC 2. *x* aplicativo chamará **SQLSetConnectOption** por meio de um ODBC 3 *. x* driver, a chamada para  
  
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
  
 Nos três casos anteriores, o *ConnectionHandle* argumento é definido como o valor na *hdbc*, o *atributo* argumento é definido como o valor em *fOption* e o *ValuePtr* argumento é definido como o mesmo valor de *vParam*.  
  
 Porque o Gerenciador de Driver não sabe se o atributo de conexão definido pelo driver precisa de uma cadeia de caracteres ou um valor de inteiro de 32 bits, ele deve passar um valor válido para o *BufferLength* argumento de **SQLSetConnectAttr**. Se o driver tiver definido a semântica especial para definido pelo driver conectar atributos e precisa ser chamado usando **SQLSetConnectOption**, ele deve suportar **SQLSetConnectOption**.  
  
 Se um ODBC 2. *x* aplicativo chamará **SQLSetConnectOption** para definir uma opção de instrução específicos de driver em um ODBC 3 *. x* driver e a opção foi definida em um ODBC 2. *x* versão do driver, uma nova constante de manifesto deve ser definido para a opção em ODBC 3 *. x* driver. Se a constante de manifesto antiga é usada na chamada para **SQLSetConnectOption**, o Gerenciador de Driver chamará **SQLSetConnectAttr** com o **StringLength** argumento definido como 0.  
  
 Para um ODBC 3 *. x* driver, o Gerenciador de Driver não verifica se *fOption* está entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX ou é maior que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Definindo opções de instrução em nível de Conexão  
 No ODBC 2. *x*, um aplicativo poderia chamar **SQLSetConnectOption** para definir uma opção de instrução. Quando isso for feito, o driver estabelece a opção de instrução por padrão para todas as instruções posteriormente alocadas para essa conexão. Ele é definido pelo driver se o driver define a opção de instrução para quaisquer instruções existentes associadas com a conexão especificada.  
  
 Essa capacidade foi preterida no ODBC 3 *. x*. 3 de ODBC *. x* drivers precisam apenas oferece suporte à definição do ODBC 2. *x* atributos de instrução no nível de conexão se eles desejam trabalhar com ODBC 2. *x* aplicativos que fazem isso. 3 de ODBC *. x* aplicativos nunca devem definir atributos de instrução no nível de conexão. 3 de ODBC *. x* atributos de instrução não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de instrução e pode ser definido no nível de conexão ou o nível de instrução.
