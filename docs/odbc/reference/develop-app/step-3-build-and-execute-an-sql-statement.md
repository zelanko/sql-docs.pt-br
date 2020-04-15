---
title: 'Passo 3: Construir e executar uma declaração SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e8322cf5e7b4a91bfc5f5f0204cfb25fa4bdad92
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81306827"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Etapa 3: Criar e executar uma instrução SQL
O terceiro passo é construir e executar uma declaração SQL, como mostrado na ilustração a seguir. Os métodos usados para realizar esta etapa provavelmente variam tremendamente. O aplicativo pode solicitar ao usuário que insira uma instrução SQL, crie uma instrução SQL com base na entrada do usuário ou use uma instrução SQL codificada. Para obter mais informações, consulte [Constructing SQL Statements](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Mostra a criação e a execução de uma instrução SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se a declaração SQL contiver parâmetros, o aplicativo os vincula às variáveis do aplicativo, chamando **SQLBindParameter** para cada parâmetro. Para obter mais informações, consulte [Parâmetros de declaração](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Depois que a declaração SQL é construída e quaisquer parâmetros são vinculados, a declaração é executada com **SQLExecDirect**. Se a declaração for executada várias vezes, ela poderá ser preparada com **o SQLPrepare** e executada com **o SQLExecute**. Para obter mais informações, consulte [Executando uma Declaração](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 O aplicativo também pode deixar de executar uma declaração SQL completamente e, em vez disso, chamar uma função para retornar um conjunto de resultados contendo informações do catálogo, como as colunas ou tabelas disponíveis. Para obter mais informações, consulte [Usos de Dados de Catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 A próxima ação do aplicativo depende do tipo de declaração SQL executada.  
  
|Tipo de declaração SQL|Proceder a|  
|---------------------------|----------------|  
|**FUNÇÃO SELECT** ou catálogo|[Etapa 4a: Buscar os resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ATUALIZAR,** **EXCLUIR**ou **INSERIR**|[Etapa 4b: Buscar a contagem de linhas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas as outras declarações SQL|Passo 3: Construir e executar uma declaração SQL (este tópico) ou [passo 5: Comprometa a transação](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
