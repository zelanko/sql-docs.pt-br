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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 5f4e17074616111ee93ce87c04036d1fc3fd48dd
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63062414"
---
# <a name="gateways-diagnostic-example"></a>Exemplo de diagnóstico de gateways
Em uma arquitetura de gateway, um driver envia solicitações a um gateway que oferece suporte ao ODBC. O gateway envia solicitações de um DBMS. Como é o componente que faz interface com o Gerenciador de Driver, o driver formata e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se o Oracle com base em um gateway para Rdb no Microsoft Open Data Services e se Rdb não foi possível encontrar a tabela funcionário, o gateway pode gerar essa mensagem de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Devido a erro na fonte de dados, o gateway adicionado um prefixo para o identificador de fonte de dados [Rdb (]) para a mensagem de diagnóstico. Como o gateway foi o componente que interagir com a fonte de dados, ele adicionou prefixos para seu fornecedor ([DEC]) e o identificador ([ODS Gateway]) para a mensagem de diagnóstico. Ele também adicionou o valor SQLSTATE e o código de erro de Rdb para o início da mensagem de diagnóstico. Isso permitido para preservar a semântica da própria estrutura de mensagem e ainda fornecer as informações de diagnóstico de ODBC para o driver. O driver analisa as informações de erro anexadas à instrução erro pelo gateway.  
  
 Como o driver de gateway é o componente que faz interface com o Gerenciador de Driver, usaria a mensagem de diagnóstico anterior para formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
