---
title: Suporte para tipos de dados (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Visual FoxPro ODBC driver [ODBC], data types
- FoxPro ODBC driver [ODBC], data types
- data types [ODBC], Visual FoxPro ODBC driver
ms.assetid: ab529cc6-d157-4b35-b6f9-6ffd09af098c
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c6baf7807f2b179f8e7eb0d383e22a39452df4fe
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de dados com suporte (Driver ODBC do Visual FoxPro)
A lista de tipos de dados com suporte pelo driver são apresentados por meio da API do ODBC e no Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de dados em aplicativos C  
 Você pode obter uma lista de tipos de dados suportados pelo Driver ODBC para Visual FoxPro, usando o [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) função em aplicativos C ou C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de dados em aplicativos que usam o Microsoft Query  
 Se seu aplicativo usa o Microsoft Query para criar uma nova tabela em uma fonte de dados do Visual FoxPro, Microsoft Query exibe o **nova definição de tabela** caixa de diálogo. Em **campo Descrição**, o **tipo** caixa listas [tipos de dados de campo do Visual FoxPro](../../odbc/microsoft/visual-foxpro-field-data-types.md)representado pelos caracteres únicos.
