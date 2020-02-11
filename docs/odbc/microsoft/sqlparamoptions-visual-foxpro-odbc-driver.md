---
title: Sqlparamoptions (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: 1adbde1b3df38d2b602f1ec42a2c96f36e8bd67b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67996379"
---
# <a name="sqlparamoptions-visual-foxpro-odbc-driver"></a>SQLParamOptions (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Permite que um aplicativo especifique vários valores para o conjunto de parâmetros atribuído por [SQLBindParameter](../../odbc/microsoft/sqlbindparameter-visual-foxpro-odbc-driver.md). A capacidade de especificar vários valores para um conjunto de parâmetros é útil para inserções em massa e outros trabalhos que exigem que a fonte de dados processe a mesma instrução SQL várias vezes com vários valores de parâmetro. Por exemplo, um aplicativo pode especificar três conjuntos de valores para o conjunto de parâmetros associados a uma instrução **Insert** e, em seguida, executar a instrução **Insert** uma vez para executar as três operações de inserção.  
  
 Para obter mais informações, consulte [Sqlparamoptions](../../odbc/reference/syntax/sqlparamoptions-function.md) na *referência do programador de ODBC*.
