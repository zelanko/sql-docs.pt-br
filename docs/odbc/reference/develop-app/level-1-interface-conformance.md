---
title: Conformidade de Interface de nível 1 | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: f2071ec7d7c9a31a9da8982b583ef7618700db5e
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47649314"
---
# <a name="level-1-interface-conformance"></a>Conformidade de interface nível 1
O nível de conformidade de interface de nível 1 inclui a funcionalidade do nível de conformidade com a interface do Core além de recursos adicionais, como transações, que geralmente estão disponíveis em um DBMS relacional de OLTP. Um driver de interface – compatível com nível 1 permite que o aplicativo faça o seguinte, além dos recursos no nível de conformidade de interface principal:  
  
|||  
|-|-|  
|101|Especifique o esquema do banco de dados de tabelas e exibições (usando a nomenclatura de duas partes). (Para obter mais informações, consulte a nomenclatura de três partes 201 de recursos [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Invocar a execução assíncrona verdadeira de funções ODBC, onde as funções aplicáveis do ODBC são todos síncrono ou assíncrono em uma determinada conexão.|  
|103|Usar cursores roláveis e, assim, obter acesso a um conjunto de resultados em métodos em vez de somente avanço, chamando **SQLFetchScroll** com o *FetchOrientation* argumento que não seja SQL_FETCH_NEXT. (O SQL_FETCH_BOOKMARK *FetchOrientation* está no recurso 204 no [conformidade de Interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Obter as chaves primárias das tabelas, chamando **SQLPrimaryKeys**.|  
|105|Use os procedimentos armazenados, por meio da sequência de escape ODBC para chamadas de procedimento e consultar o dicionário de dados em relação a procedimentos armazenados, chamando **SQLProcedureColumns** e **SQLProcedures**. (O processo pelo qual os procedimentos são criados e armazenados na fonte de dados está fora do escopo deste documento.)|  
|106|Conectar a uma fonte de dados navegando interativamente os servidores disponíveis, chamando **SQLBrowseConnect**.|  
|107|Usar funções ODBC em vez de instruções SQL para executar determinadas operações de banco de dados: **SQLSetPos** com SQL_POSITION e SQL_REFRESH.|  
|108|Obter acesso ao conteúdo de vários conjuntos de resultados gerados por lotes e procedimentos armazenados, chamando **SQLMoreResults**.|  
|109|Delimite as transações que abrangem várias funções ODBC com true atomicidade e a capacidade de especificar SQL_ROLLBACK na **SQLEndTran**.|
