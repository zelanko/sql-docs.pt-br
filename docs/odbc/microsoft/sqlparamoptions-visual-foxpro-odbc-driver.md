---
title: SQLParamOptions (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLParamOptions function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 7f94a6e2-9c34-405c-b2b0-304d94269715
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a66f0cd3a17baa9a09a5eeef2ade3d730f0a206b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636655"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 1  
  
 Permite que um aplicativo especifique vários valores para o conjunto de parâmetros atribuído pelo [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). A capacidade de especificar vários valores para um conjunto de parâmetros é útil para inserções em massa e outro trabalho que requer que a fonte de dados para processar a mesma instrução SQL várias vezes com vários valores de parâmetro. Por exemplo, um aplicativo pode especificar três conjuntos de valores para o conjunto de parâmetros associados a um **inserir** instrução e, em seguida, execute o **inserir** Inserir instrução uma vez para executar os três operações.  
  
 Para obter mais informações, consulte [SQLParamOptions](../../odbc/reference/syntax/sqlparamoptions-function.md) na *referência do programador de ODBC*.
