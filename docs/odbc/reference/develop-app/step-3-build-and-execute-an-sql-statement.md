---
title: 'Etapa 3: criar e executar uma instrução SQL | Microsoft Docs'
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: f0e369b74ef629c5fd7136b9098f579b5ad2b1b4
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68114258"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Etapa 3: Criar e executar uma instrução SQL
A terceira etapa é criar e executar uma instrução SQL, conforme mostrado na ilustração a seguir. Os métodos usados para executar essa etapa provavelmente variam enormemente. O aplicativo pode solicitar que o usuário insira uma instrução SQL, criar uma instrução SQL com base na entrada do usuário ou usar uma instrução SQL embutida em código. Para obter mais informações, consulte [construindo instruções SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Mostra a criação e a execução de uma instrução SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se a instrução SQL contiver parâmetros, o aplicativo os associará a variáveis de aplicativo chamando **SQLBindParameter** para cada parâmetro. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Depois que a instrução SQL é criada e quaisquer parâmetros são associados, a instrução é executada com **SQLExecDirect**. Se a instrução for executada várias vezes, ela poderá ser preparada com **SQLPrepare** e executada com **SQLExecute**. Para obter mais informações, consulte [executando uma instrução](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 O aplicativo também pode abrem mão executar uma instrução SQL completamente e, em vez disso, chamar uma função para retornar um conjunto de resultados contendo informações do catálogo, como as colunas ou tabelas disponíveis. Para obter mais informações, consulte [usos de dados do catálogo](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 A próxima ação do aplicativo depende do tipo de instrução SQL executada.  
  
|Tipo de instrução SQL|Vá para|  
|---------------------------|----------------|  
|Função **Select** ou Catalog|[Etapa 4a: Buscar os resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**Atualizar**, **excluir**ou **Inserir**|[Etapa 4b: Buscar a contagem de linhas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas as outras instruções SQL|Etapa 3: criar e executar uma instrução SQL (este tópico) ou a [etapa 5: confirmar a transação](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
