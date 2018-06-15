---
title: 'Etapa 3: Criar e executar uma instrução SQL | Microsoft Docs'
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- application process [ODBC], building and executing statements
- SQL statements [ODBC], building and executing
ms.assetid: 133b8bd4-a3c8-4f7e-93c5-c05283c8e96f
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f972fb5a0edfbbf492860e3421d5985d5e4edcc
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32915501"
---
# <a name="step-3-build-and-execute-an-sql-statement"></a>Etapa 3: Criar e executar uma instrução SQL
A terceira etapa é criar e executar uma instrução SQL, conforme mostrado na ilustração a seguir. Os métodos usados para executar essa etapa serão prováveis podem variar muito. O aplicativo pode solicitar que o usuário insira uma instrução SQL, crie uma instrução SQL com base na entrada do usuário, ou usar uma instrução SQL embutido. Para obter mais informações, consulte [construindo instruções de SQL](../../../odbc/reference/develop-app/constructing-sql-statements.md).  
  
 ![Mostra a criação e execução de uma instrução SQL](../../../odbc/reference/develop-app/media/pr13.gif "pr13")  
  
 Se a instrução SQL contiver parâmetros, o aplicativo associa a variáveis de aplicativo chamando **SQLBindParameter** para cada parâmetro. Para obter mais informações, consulte [parâmetros de instrução](../../../odbc/reference/develop-app/statement-parameters.md).  
  
 Após a instrução SQL é criada e todos os parâmetros associados, a instrução é executada com **SQLExecDirect**. Se a instrução for executada várias vezes, pode ser preparado com **SQLPrepare** e são executados com **SQLExecute**. Para obter mais informações, consulte [executando uma instrução](../../../odbc/reference/develop-app/executing-a-statement.md).  
  
 O aplicativo pode também abrir mão de executar uma instrução SQL completamente e chamar uma função para retornar um conjunto de resultados que contém informações de catálogo, como as tabelas ou colunas disponíveis. Para obter mais informações, consulte [usa do catálogo de dados](../../../odbc/reference/develop-app/uses-of-catalog-data.md).  
  
 Ação próxima do aplicativo depende do tipo de instrução SQL executada.  
  
|Tipo de instrução SQL|Vá para|  
|---------------------------|----------------|  
|**Selecione** ou função de catálogo|[Etapa 4a: Buscar os resultados](../../../odbc/reference/develop-app/step-4a-fetch-the-results.md)|  
|**ATUALIZAÇÃO**, **excluir**, ou **inserir**|[Etapa 4b: Buscar a contagem de linhas](../../../odbc/reference/develop-app/step-4b-fetch-the-row-count.md)|  
|Todas as outras instruções SQL|Etapa 3: Criar e executar uma instrução SQL (Este tópico) ou [etapa 5: confirmar a transação](../../../odbc/reference/develop-app/step-5-commit-the-transaction.md)|
