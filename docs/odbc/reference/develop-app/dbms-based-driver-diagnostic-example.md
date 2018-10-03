---
title: Exemplo de diagnóstico de Driver baseado em DBMS | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 0485ecf720cb84580c17c77b31fc6816de2e679a
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47622264"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em DBMS
Um driver baseados em DBMS envia solicitações para um DBMS e retorna as informações do aplicativo por meio do Gerenciador de Driver. Como o driver é o componente que faz interface com o Gerenciador de Driver, formata e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se, usando o SQL/Services, um driver da Microsoft para Oracle Rdb encontrou um nome de cursor inválido, ele pode retornar os seguintes valores **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Como o erro ocorreu no driver, adicionado prefixos para a mensagem de diagnóstico para o fornecedor ([Microsoft]) e o driver ([ODBC Rdb Driver]).  
  
 Se o DBMS não foi possível encontrar a tabela funcionário, o driver pode formatar e retornar os seguintes valores **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Devido a erro na fonte de dados, o driver adicionado um prefixo para o identificador de fonte de dados [Rdb (]) para a mensagem de diagnóstico. Como o driver foi o componente que interagir com a fonte de dados, ele adicionou prefixos para seu fornecedor ([Microsoft]) e o identificador ([ODBC Rdb Driver]) para a mensagem de diagnóstico.
