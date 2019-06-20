---
title: SQLPrimaryKeys (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLPrimaryKeys function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 8dbe2903-efdc-45e0-a079-9e357c5fd81b
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3eeafa338fea31741609e6f9a9b32a4128ebd87d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62636325"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas de Driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado sob [referência da API ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte a: Completo  
  
 Conformidade com a API ODBC: Nível 2  
  
 Retorna os nomes das colunas que compõem a chave primária para uma tabela. A implementação do Driver ODBC do Visual FoxPro do **SQLPrimaryKeys** se comporta da seguinte maneira:  
  
-   Ignora a *szTableOwner* e *cbTableOwner* argumentos.  
  
-   Funciona somente para fontes de dados que são [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md). O driver retorna "Driver não oferece suporte a essa função" o erro se a fonte de dados é um diretório do [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obter mais informações, consulte [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) na *referência do programador de ODBC*.
