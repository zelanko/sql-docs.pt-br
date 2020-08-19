---
description: Exemplo de diagnóstico de driver baseado em DBMS
title: Exemplo de diagnóstico de driver baseado em DBMS | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5425afb18a5582a840966798ea7a7209dba7e1e6
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88424738"
---
# <a name="dbms-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em DBMS
Um driver baseado em DBMS envia solicitações para um DBMS e retorna informações para o aplicativo por meio do Gerenciador de driver. Como o driver é o componente que faz interface com o Gerenciador de driver, ele formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se, usando SQL/Services, um driver da Microsoft para Oracle RDB tiver encontrado um nome de cursor inválido, ele poderá retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "34000"  
Native Error:      0  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver]Invalid cursor name: EMPLOYEE_CURSOR."  
```  
  
 Como o erro ocorreu no driver, ele adicionou prefixos à mensagem de diagnóstico para o fornecedor ([Microsoft]) e o driver ([Driver do ODBC RDB]).  
  
 Se o DBMS não pôde localizar o funcionário da tabela, o driver pode formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[Microsoft][ODBC Rdb Driver][Rdb] %SQL-F-RELNOTDEF, Table EMPLOYEE "  
                  "is not defined in schema."  
```  
  
 Como o erro ocorreu na fonte de dados, o driver adicionou um prefixo para o identificador de fonte de dados ([RDB]) à mensagem de diagnóstico. Como o driver era o componente que interfrenteu com a fonte de dados, ele adicionou prefixos para seu fornecedor ([Microsoft]) e identificador ([Driver do ODBC RDB]) à mensagem de diagnóstico.
