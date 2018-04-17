---
title: Exemplo de diagnóstico de gateways | Microsoft Docs
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
ms.topic: article
helpviewer_keywords:
- diagnostic information [ODBC], examples
- gateway diagnostic [ODBC]
- error messages [ODBC], diagnostic messages
ms.assetid: e0695fac-4593-4b3d-8675-cb8f73dab966
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 8c8e7edec0e2af7c7c2645e2e9fbc021acf8ceab
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="gateways-diagnostic-example"></a>Exemplo de diagnóstico de gateways
Em uma arquitetura de gateway, um driver envia solicitações para um gateway que ofereça suporte a ODBC. O gateway envia as solicitações para um DBMS. Porque é o componente que faz interface com o Gerenciador de Driver, o driver formata e retorna os argumentos para **SQLGetDiagRec**.  
  
 Por exemplo, se o Oracle com base em um gateway para Rdb no Microsoft Open Data Services e se Rdb não foi possível encontrar a tabela funcionário, o gateway pode gerar essa mensagem de diagnóstico:  
  
```  
"[42S02][-1][DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not defined "  
   "in schema."  
```  
  
 Devido ao erro na fonte de dados, o gateway adicionado um prefixo para o identificador de fonte de dados ([Rdb]) para a mensagem de diagnóstica. Como o gateway foi o componente de interagir com a fonte de dados, ele adicionou prefixos para seu fornecedor ([DEC]) e o identificador ([Gateway ODS]) à mensagem de diagnóstico. Ele também adicionou o valor SQLSTATE e o código de erro Rdb até o início da mensagem de diagnóstico. Isso permitido para preservar a semântica da sua própria estrutura de mensagens e ainda fornecer as informações de diagnóstico de ODBC para o driver. O driver analisa as informações de erro anexadas à instrução erro pelo gateway.  
  
 Como o driver de gateway é o componente que faz interface com o Gerenciador de Driver, ele usaria a mensagem de diagnóstica anterior para formatar e retornar os seguintes valores de **SQLGetDiagRec**:  
  
```  
SQLSTATE:         "42S02"  
Native Error:      -1  
Diagnostic Msg:   "[DEC][ODS Gateway][Rdb]%SQL-F-RELNOTDEF, Table EMPLOYEE is not "  
                  "defined in schema."  
```
