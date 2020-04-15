---
title: Conformidade de interface nível 1 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- interface conformance levels [ODBC]
- conformance levels [ODBC], interface
- level 1 interface conformance levels [ODBC]
ms.assetid: ee3f5c08-0583-4f3b-8354-ef71b6086a7e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3d31d5fe8aea1df4e7937104580efb820ba6f031
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306177"
---
# <a name="level-1-interface-conformance"></a>Conformidade de interface nível 1
O nível de conformidade da interface Nível 1 inclui a funcionalidade do nível de conformidade da interface Core, além de recursos adicionais, como transações, que geralmente estão disponíveis em um DBMS relacional OLTP. Um driver de conformidade de interface Nível 1 permite que o aplicativo faça o seguinte, além dos recursos no nível de conformidade da interface Core:  
  
|||  
|-|-|  
|101|Especifique o esquema de tabelas e visualizações de banco de dados (usando nomeação em duas partes). (Para obter mais informações, consulte o recurso de nomeação em três partes 201 no [Nível 2 De Conformidade de Interface](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Invoque a verdadeira execução assíncrona das funções ODBC, onde as funções ODBC aplicáveis são todas síncronas ou todas assíncronas em uma determinada conexão.|  
|103|Use cursores roláveis e, assim, obtenha acesso a um conjunto de resultados em métodos diferentes apenas para frente, chamando **SQLFetchScroll** com o argumento *FetchOrientation* diferente de SQL_FETCH_NEXT. (O SQL_FETCH_BOOKMARK *FetchOrientation* está no recurso 204 na [Conformidade de Interface Nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Obtenha as chaves primárias das tabelas, chamando **SQLPrimaryKeys**.|  
|105|Use os procedimentos armazenados, através da seqüência de fuga do ODBC para chamadas de procedimento, e consulte o dicionário de dados sobre procedimentos armazenados, ligando para **SQLProcedureColumns** e **SQLProcedures**. (O processo pelo qual os procedimentos são criados e armazenados na fonte de dados está fora do escopo deste documento.)|  
|106|Conecte-se a uma fonte de dados navegando interativamente nos servidores disponíveis, ligando para **O SQLBrowseConnect**.|  
|107|Use funções ODBC em vez de instruções SQL para executar certas operações de banco de dados: **SQLSetPos** com SQL_POSITION e SQL_REFRESH.|  
|108|Obtenha acesso ao conteúdo de vários conjuntos de resultados gerados por lotes e procedimentos armazenados, ligando para **SQLMoreResults**.|  
|109|Delimitar transações abrangendo várias funções ODBC, com a verdadeira atônidade e a capacidade de especificar SQL_ROLLBACK no **SQLEndTran**.|
