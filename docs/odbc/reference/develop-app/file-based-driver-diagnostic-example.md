---
description: Exemplo de diagnóstico de driver baseado em arquivo
title: Exemplo de diagnóstico de driver baseado em arquivo | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- file-based driver diagnostic [ODBC]
- diagnostic information [ODBC], examples
- error messages [ODBC], diagnostic messages
ms.assetid: 0575fccd-4641-478d-a3cc-5a764e35bae2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 8986ebaa8c4ecf0ac18f4e043eb731df35054884
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88499856"
---
# <a name="file-based-driver-diagnostic-example"></a>Exemplo de diagnóstico de driver baseado em arquivo
Um driver baseado em arquivo atua como um driver ODBC e como uma fonte de dados. Portanto, isso pode gerar erros e avisos como um componente em uma conexão ODBC e como uma fonte de dados. Como ele também é o componente que faz interface com o Gerenciador de driver, ele formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se um driver do Microsoft® para dBASE não pôde alocar memória suficiente, ele pode retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "HY001"  
Native Error:      42052  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver]Unable to allocate sufficient memory."  
```  
  
 Como esse erro não estava relacionado à fonte de dados, o driver adicionou apenas prefixos à mensagem de diagnóstico para o fornecedor ([Microsoft]) e o driver ([Driver do dBASE ODBC]).  
  
 Se o driver não pôde localizar o arquivo Employee. dbf, ele pode retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1305  
Diagnostic Msg:   "[Microsoft][ODBC dBASE Driver][dBASE]No such table or object"  
```  
  
 Como esse erro estava relacionado à fonte de dados, o driver adicionou o formato de arquivo da fonte de dados ([dBASE]) como um prefixo à mensagem de diagnóstico. Como o driver também era o componente que interfrenteu com a fonte de dados, ele adicionou prefixos para o fornecedor ([Microsoft]) e o driver ([Driver dBASE do ODBC]).
