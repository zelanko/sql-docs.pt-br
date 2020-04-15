---
title: Exemplo de diagnóstico de gateways | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: b18fd78be7be2eb79316339cbdf3d315deb194fb
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81305567"
---
# <a name="gateways-diagnostic-example"></a>Exemplo de diagnóstico de gateways
Em uma arquitetura de gateway, um driver envia solicitações para um gateway que suporta ODBC. O gateway envia as solicitações para um DBMS. Como é o componente que faz interface com o Driver Manager, o driver formata e retorna argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se o Oracle baseou um gateway para rdb no Microsoft Open Data Services e se o Rdb não conseguiu encontrar a tabela EMPLOYEE, o gateway pode gerar essa mensagem de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Como o erro ocorreu na fonte de dados, o gateway adicionou um prefixo para o identificador de origem de dados ([Rdb]) à mensagem de diagnóstico. Como o gateway era o componente que interagia com a fonte de dados, ele adicionou prefixos para seu fornecedor ([DEC]) e identificador ([ODS Gateway]) à mensagem de diagnóstico. Também adicionou o valor SQLSTATE e o código de erro Rdb ao início da mensagem de diagnóstico. Isso permitiu preservar a semântica de sua própria estrutura de mensagem e ainda fornecer as informações de diagnóstico da ODBC ao motorista. O motorista analisa as informações de erro anexadas à declaração de erro pelo gateway.  
  
 Como o driver gateway é o componente que interage com o Driver Manager, ele usaria a mensagem de diagnóstico anterior para formatar e retornar os seguintes valores do **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
