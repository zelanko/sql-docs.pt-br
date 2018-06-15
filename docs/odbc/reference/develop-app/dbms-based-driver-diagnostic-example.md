---
title: Exemplo de diagnóstico baseados em DBMS Driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- DBMS-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: a80d54b0-43ff-4dfd-b6cb-f4694a5ed765
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2f26421a71edad627dcc4d89c854dbafa78766
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32910841"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de drivers baseados em DBMS
Um driver de DBMS envia solicitações para um DBMS e retorna informações para o aplicativo por meio do Gerenciador de Driver. Como o driver é o componente que faz interface com o Gerenciador de Driver, formatos e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se usando SQL/Services, um driver da Microsoft para Oracle Rdb encontrou um nome de cursor inválido, ele pode retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Devido ao erro no driver, adicionado prefixos à mensagem de diagnóstico para o fornecedor ([Microsoft]) e o driver ([ODBC Rdb Driver]).  
  
 Se o DBMS não foi possível encontrar a tabela funcionário, o driver pode formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Devido ao erro na fonte de dados, o driver adicionado um prefixo para o identificador de fonte de dados ([Rdb]) para a mensagem de diagnóstica. Como o driver foi o componente de interagir com a fonte de dados, ele adicionou prefixos para seu fornecedor ([Microsoft]) e o identificador ([ODBC Rdb Driver]) à mensagem de diagnóstico.
