---
title: Conformidade de interface nível 2 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- level 2 interface conformance levels [ODBC]
- conformance levels [ODBC], interface
ms.assetid: 2dc87840-f2fe-43dd-9d7b-bd95523081d9
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3ee57d716cbb93f855e1fd78d41bff62a681eb6c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306157"
---
# <a name="level-2-interface-conformance"></a>Conformidade de interface nível 2
O nível de conformidade da interface Nível 2 inclui a funcionalidade nível de conformidade da interface Nível 1, além dos seguintes recursos:  
  
|||  
|-|-|  
|201|Use nomes de três partes de tabelas e visualizações de banco de dados. (Para obter mais informações, consulte o recurso de suporte de nomeação em duas partes 101 no [Nível 1 De conformidade de interface](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Descreva parâmetros dinâmicos, chamando **SQLDescribeParam**.|  
|203|Use não apenas parâmetros de entrada, mas também parâmetros de saída e entrada/saída e valores de resultado dos procedimentos armazenados.|  
|204|Use marcadores, incluindo a recuperação de marcadores, ligando para **SQLDescribeCol** e **SQLColAttribute** na coluna número 0; buscar com base em um marcador, chamando **SQLFetchScroll** com o argumento *FetchOrientation* definido para SQL_FETCH_BOOKMARK; e atualize, exclua e busque por operações de marcadores, ligando para **SQLBulkOperations** com o argumento *Operação* definido para SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK.|  
|205|Recupere informações avançadas sobre o dicionário de dados, chamando **SQLColumnPrivileges,** **SQLForeignKeys**e **SQLTablePrivileges**.|  
|206|Use funções ODBC em vez de instruções SQL para executar operações adicionais de banco de dados, ligando para **SQLBulkOperations** com SQL_ADD ou **SQLSetPos** com SQL_DELETE ou SQL_UPDATE. (O suporte para chamadas para **SQLSetPos** com o argumento *LockType* definido para SQL_LOCK_EXCLUSIVE ou SQL_LOCK_UNLOCK não faz parte dos níveis de conformidade, mas é um recurso opcional.)|  
|207|Habilite a execução assíncrona das funções ODBC para instruções individuais especificadas.|  
|208|Obtenha a SQL_ROWVER coluna de identificação de linhas de tabelas, ligando para **SQLSpecialColumns**. (Para obter mais informações, consulte o suporte para **SQLSpecialColumns** com o argumento *IdentifierType* definido para SQL_BEST_ROWID como recurso 20 na [Conformidade de Interface Principal](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|Defina o atributo de declaração SQL_ATTR_CONCURRENCY para pelo menos um valor diferente SQL_CONCUR_READ_ONLY.|  
|210|A capacidade de cronometrar a solicitação de login e as consultas SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|A capacidade de alterar o nível de isolamento padrão; a capacidade de executar transações com o nível "serializável" de isolamento.|
