---
title: "Conformidade de Interface de nível 2 | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: c272637e15d95a09862170ec871274adb624c271
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="level-2-interface-conformance"></a>Conformidade de Interface de nível 2
O nível de conformidade de interface de nível 2 inclui a funcionalidade de conformidade de nível de interface de nível 1 além dos seguintes recursos:  
  
|||  
|-|-|  
|201|Use nomes de três partes de tabelas de banco de dados e exibições. (Para obter mais informações, consulte o duas partes suporte ao recurso de nomeação 101 em [nível 1 Interface conformidade](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Descrever os parâmetros dinâmicos, chamando **SQLDescribeParam**.|  
|203|Use não apenas parâmetros de entrada, mas também os parâmetros de saída e entrada/saída e valores de resultado de procedimentos armazenados.|  
|204|Usar indicadores, incluindo a recuperação de indicadores, chamando **SQLDescribeCol** e **SQLColAttribute** na coluna de número 0; busca com base em um indicador, chamando **SQLFetchScroll** com o *FetchOrientation* argumento definido como SQL_FETCH_BOOKMARK; e atualizar, excluir e buscar por operações de indicador, chamando **SQLBulkOperations** com o *Operação* argumento definido como SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK.|  
|205|Recuperar informações avançadas sobre o dicionário de dados, chamando **SQLColumnPrivileges**, **SQLForeignKeys**, e **SQLTablePrivileges**.|  
|206|Use funções ODBC em vez de instruções SQL para executar operações de banco de dados adicionais, chamando **SQLBulkOperations** com SQL_ADD, ou **SQLSetPos** com SQL_DELETE ou SQL_UPDATE. (Suporte a chamadas para **SQLSetPos** com o *LockType* argumento definido como SQL_LOCK_EXCLUSIVE ou SQL_LOCK_UNLOCK não é uma parte dos níveis de conformidade, mas é um recurso opcional.)|  
|207|Habilite a execução assíncrona de funções ODBC para instruções individuais especificadas.|  
|208|Obter a coluna de identificação de linha SQL_ROWVER de tabelas, chamando **SQLSpecialColumns**. (Para obter mais informações, consulte o suporte para **SQLSpecialColumns** com o *IdentifierType* argumento definido como SQL_BEST_ROWID como recurso 20 no [Core Interface conformidade](../../../odbc/reference/develop-app/core-interface-conformance.md) .)|  
|209|Defina o atributo de instrução SQL_ATTR_CONCURRENCY como pelo menos um valor diferente de SQL_CONCUR_READ_ONLY.|  
|210|A capacidade de solicitação de logon de tempo limite e consultas SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|A capacidade de alterar o nível de isolamento padrão; a capacidade de executar as transações com o "serializável" nível de isolamento.|
