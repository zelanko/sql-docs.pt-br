---
title: Suporte para tipos de dados (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6e80a4f6f079620e4a5a3ee82d87342e87591001
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de dados com suporte (Driver ODBC do Visual FoxPro)
A lista de tipos de dados com suporte pelo driver são apresentados por meio da API do ODBC e no Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de dados em aplicativos C  
 Você pode obter uma lista de tipos de dados suportados pelo Driver ODBC para Visual FoxPro, usando o [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) função em aplicativos C ou C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de dados em aplicativos que usam o Microsoft Query  
 Se seu aplicativo usa o Microsoft Query para criar uma nova tabela em uma fonte de dados do Visual FoxPro, Microsoft Query exibe o **nova definição de tabela** caixa de diálogo. Em **campo Descrição**, o **tipo** caixa listas [tipos de dados de campo do Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md)representado pelos caracteres únicos.
