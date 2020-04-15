---
title: Mapeamento de opção sqlsetconnect | Microsoft Docs
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
ms.openlocfilehash: 757b50c7e18133e02b4cf6addaa327b2053f5439
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81287466"
---
# <a name="sqlsetconnectoption-mapping"></a>Mapeamento SQLSetConnectOption
Quando um ODBC 2. *x* aplicativo chama **SQLSetConnectOption** através de um driver ODBC 3 *.x,* a chamada para  
  
```  
SQLSetConnectOption(hdbc, fOption, vParam)  
```  
  
 resultará da seguinte forma:  
  
-   Se *fOption* indicar um atributo de conexão definido pelo ODBC que requer uma seqüência de strings, o Gerenciador de driver saqueia  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, SQL_NTS)  
    ```  
  
-   Se *fOption* indicar um atributo de conexão definido pelo ODBC que retorna um valor inteiro de 32 bits, o Gerenciador de driver seleção chama  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, 0)  
    ```  
  
-   Se *fOption* indicar um atributo de conexão definido pelo driver, o Gerenciador de driver saqueia  
  
    ```  
    SQLSetConnectAttr(ConnectionHandle, Attribute, ValuePtr, BufferLength)  
    ```  
  
 Nos três casos anteriores, o argumento *ConnectionHandle* é definido como o valor em *hdbc*, o argumento *Atributo* é definido como o valor em *fOption*, e o argumento *ValuePtr* é definido para o mesmo valor que *vParam*.  
  
 Como o Gerenciador de driver não sabe se o atributo de conexão definido pelo driver precisa de um valor inteiro de string ou 32 bits, ele tem que passar em um valor válido para o argumento *BufferLength* do **SQLSetConnectAttr**. Se o driver tiver definido a semântica especial para atributos de conexão definidos pelo driver e precisar ser chamado usando **SQLSetConnectOption,** ele deve suportar **SQLSetConnectOption**.  
  
 Se um ODBC 2. *x* aplicativo chama **SQLSetConnectOption** para definir uma opção de instrução específica do driver em um driver ODBC 3 *.x,* e a opção foi definida em um ODBC 2. *x* versão do driver, uma nova constante de manifesto deve ser definida para a opção no driver ODBC 3 *.x.* Se a antiga constante de manifesto for usada na chamada para **SQLSetConnectOption,** o Driver Manager chamará **SQLSetConnectAttr** com o argumento **StringLength** definido como 0.  
  
 Para um driver ODBC 3 *.x,* o Driver Manager não verifica mais se *fOption* está entre SQL_CONN_OPT_MIN e SQL_CONN_OPT_MAX, ou se é maior do que SQL_CONNECT_OPT_DRVR_START.  
  
## <a name="setting-statement-options-on-the-connection-level"></a>Definindo opções de declaração no nível de conexão  
 Em ODBC 2. *x*, um aplicativo pode chamar **SQLSetConnectOption** para definir uma opção de declaração. Quando isso é feito, o driver estabelece a opção de declaração como padrão para quaisquer declarações posteriores alocadas para essa conexão. É definido pelo driver se o driver define a opção de instrução para quaisquer instruções existentes associadas à conexão especificada.  
  
 Esta habilidade foi preterida em ODBC 3 *.x*. Os drivers ODBC 3 *.x* só precisam de suporte para definir o ODBC 2. *x* atributos de declaração no nível de conexão se eles quiserem trabalhar com ODBC 2. *x* aplicações que fazem isso. Os aplicativos ODBC 3 *.x* nunca devem definir atributos de declaração no nível de conexão. Os atributos de declaração ODBC 3 *.x* não podem ser definidos no nível de conexão, com exceção dos atributos SQL_ATTR_METADATA_ID e SQL_ATTR_ASYNC_ENABLE, que são atributos de conexão e atributos de declaração, e podem ser definidos tanto no nível de conexão quanto no nível de declaração.
