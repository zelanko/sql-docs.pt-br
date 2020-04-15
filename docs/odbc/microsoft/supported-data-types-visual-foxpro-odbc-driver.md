---
title: Tipos de dados suportados (driver Visual FoxPro ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 3fc28464a7c14f9801473cc125b0e90c50247d68
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301096"
---
# <a name="supported-data-types-visual-foxpro-odbc-driver"></a>Tipos de dados com suporte (Driver ODBC do Visual FoxPro)
A lista de tipos de dados suportados pelo driver são apresentadas através da API ODBC e no Microsoft Query.  
  
## <a name="data-types-in-c-applications"></a>Tipos de dados em aplicativos C  
 Você pode obter uma lista de tipos de dados suportados pelo Driver Visual FoxPro ODBC usando a função [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) em aplicativos C ou C++.  
  
## <a name="data-types-in-applications-using-microsoft-query"></a>Tipos de dados em aplicativos usando o Microsoft Query  
 Se o aplicativo usar o Microsoft Query para criar uma nova tabela em uma fonte de dados Visual FoxPro, o Microsoft Query exibirá a caixa de diálogo Nova definição de **tabela.** Em **Descrição de campo,** a caixa **Tipo** lista os tipos de dados de campo [Visual FoxPro,](../../odbc/microsoft/visual-foxpro-field-data-types.md)representados por caracteres únicos.
