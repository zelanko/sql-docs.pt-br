---
title: Conformidade da interface nível 2 | Microsoft Docs
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
ms.openlocfilehash: 3b8c18a77cfd843a6bb7b70494e62dcb9efc4582
ms.sourcegitcommit: 99f61724de5edf6640efd99916d464172eb23f92
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/28/2020
ms.locfileid: "87363386"
---
# <a name="level-2-interface-conformance"></a>Conformidade de interface nível 2
O nível de conformidade da interface de nível 2 inclui a funcionalidade de nível de conformidade de interface de nível 1, além dos seguintes recursos:  
  
|Número do recurso|Descrição|  
|-|-|  
|201|Use nomes de três partes de tabelas e exibições de banco de dados. (Para obter mais informações, consulte o recurso de suporte de nomenclatura de duas partes 101 na [conformidade da interface de nível 1](../../../odbc/reference/develop-app/level-1-interface-conformance.md).)|  
|202|Descreva os parâmetros dinâmicos chamando **SQLDescribeParam**.|  
|203|Use os parâmetros de entrada não apenas, mas também os parâmetros de saída e de entrada/saída e os valores de resultado de procedimentos armazenados.|  
|204|Use indicadores, incluindo a recuperação de indicadores, chamando **SQLDescribeCol** e **SQLColAttribute** na coluna número 0; buscando com base em um indicador, chamando **SQLFetchScroll** com o argumento *FetchOrientation* definido como SQL_FETCH_BOOKMARK; e atualizar, excluir e buscar por operações de indicador chamando **SQLBulkOperations** com o argumento de *operação* definido como SQL_UPDATE_BY_BOOKMARK, SQL_DELETE_BY_BOOKMARK ou SQL_FETCH_BY_BOOKMARK.|  
|205|Recupere informações avançadas sobre o dicionário de dados, chamando **SQLColumnPrivileges**, **SQLForeignKeys**e **SQLTablePrivileges**.|  
|206|Use funções ODBC em vez de instruções SQL para executar operações de banco de dados adicionais, chamando **SQLBulkOperations** com SQL_ADD ou **SQLSetPos** com SQL_DELETE ou SQL_UPDATE. (O suporte para chamadas para **SQLSetPos** com o argumento *LockType* definido como SQL_LOCK_EXCLUSIVE ou SQL_LOCK_UNLOCK não é uma parte dos níveis de conformidade, mas é um recurso opcional.)|  
|207|Habilitar a execução assíncrona de funções ODBC para instruções individuais especificadas.|  
|208|Obtenha a SQL_ROWVER coluna de identificação de linha de tabelas, chamando **SQLSpecialColumns**. (Para obter mais informações, consulte o suporte para **SQLSpecialColumns** com o argumento *IdentifierType* definido como SQL_BEST_ROWID como o recurso 20 na [conformidade da interface principal](../../../odbc/reference/develop-app/core-interface-conformance.md).)|  
|209|Defina o atributo da instrução SQL_ATTR_CONCURRENCY para pelo menos um valor diferente de SQL_CONCUR_READ_ONLY.|  
|210|A capacidade de atingir o tempo limite de solicitações de logon e consultas SQL (SQL_ATTR_LOGIN_TIMEOUT e SQL_ATTR_QUERY_TIMEOUT).|  
|211|A capacidade de alterar o nível de isolamento padrão; a capacidade de executar transações com o nível de isolamento "serializável".|
