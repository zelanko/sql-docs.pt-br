---
description: Conformidade de interface nível 1
title: Conformidade de interface de nível 1 | Microsoft Docs
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
ms.openlocfilehash: e92b68c9e8864e79c495c9405f905fa5a4f37acf
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88476568"
---
# <a name="level-1-interface-conformance"></a>Conformidade de interface nível 1
O nível de conformidade da interface de nível 1 inclui a funcionalidade de nível de conformidade da interface principal, além de recursos adicionais, como transações, que geralmente estão disponíveis em um DBMS relacional do OLTP. Um driver compatível com a interface de nível 1 permite que o aplicativo faça o seguinte, além dos recursos do nível de conformidade da interface principal:  
  
|Número do recurso|Descrição|  
|-|-|  
|101|Especifique o esquema de tabelas e exibições de banco de dados (usando a nomeação de duas partes). (Para obter mais informações, consulte o recurso de nomenclatura de três partes 201 na [conformidade da interface de nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|102|Invocar a execução assíncrona real de funções ODBC, onde as funções ODBC aplicáveis são todas síncronas ou todas assíncronas em uma determinada conexão.|  
|103|Use cursores roláveis e, assim, obtenha acesso a um conjunto de resultados em métodos diferentes de somente encaminhamento, chamando **SQLFetchScroll** com o argumento *FetchOrientation* diferente de SQL_FETCH_NEXT. (O SQL_FETCH_BOOKMARK *FetchOrientation* está no recurso 204 na [conformidade da interface nível 2](../../../odbc/reference/develop-app/level-2-interface-conformance.md).)|  
|104|Obtenha chaves primárias de tabelas chamando **SQLPrimaryKeys**.|  
|105|Use procedimentos armazenados, por meio da sequência de escape ODBC para chamadas de procedimento e consulte o dicionário de dados em relação a procedimentos armazenados, chamando **SQLProcedureColumns** e **SQLProcedures**. (O processo pelo qual os procedimentos são criados e armazenados na fonte de dados está fora do escopo deste documento.)|  
|106|Conecte-se a uma fonte de dados navegando interativamente nos servidores disponíveis, chamando **SQLBrowseConnect**.|  
|107|Use funções ODBC em vez de instruções SQL para executar determinadas operações de banco de dados: **SQLSetPos** com SQL_POSITION e SQL_REFRESH.|  
|108|Obter acesso ao conteúdo de vários conjuntos de resultados gerados por lotes e procedimentos armazenados, chamando **SQLMoreResults**.|  
|109|Delimite as transações que abrangem várias funções ODBC, com atomicidade real e a capacidade de especificar SQL_ROLLBACK em **SQLEndTran**.|
