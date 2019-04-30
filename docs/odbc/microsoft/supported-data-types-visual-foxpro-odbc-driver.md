---
title: Suporte para tipos de dados (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 7cb48c5a763162685060a95e8d352ebddd8b0032
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63270895"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de dados com suporte (Driver ODBC do Visual FoxPro)
A lista de tipos de dados com suporte pelo driver são apresentados por meio da API do ODBC e no Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de dados em aplicativos C  
 Você pode obter uma lista dos tipos de dados suportados pelo Driver de ODBC do Visual FoxPro, usando o [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) função em aplicativos C ou C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de dados em aplicativos que usam o Microsoft Query  
 Se seu aplicativo usa o Microsoft Query para criar uma nova tabela em uma fonte de dados do Visual FoxPro, Microsoft Query exibe a **nova definição da tabela** caixa de diálogo. Sob **descrição do campo**, o **tipo** caixa listas [tipos de dados de campo do Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md)representado pelos caracteres únicos.
