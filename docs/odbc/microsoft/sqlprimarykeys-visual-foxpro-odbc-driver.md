---
title: Chaves SQLPrimary (driver Visual FoxPro ODBC) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 83631d22bd07017c4eba8f6af171443ab8c76d9c
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81301541"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver Visual FoxPro ODBC. Para obter informações gerais sobre esta função, consulte o tópico apropriado em [Referência à API oDBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: Completo  
  
 Conformidade da API ODBC: Nível 2  
  
 Retorna os nomes da coluna que compõem a chave principal de uma tabela. A implementação do Driver Visual FoxPro ODBC do **SQLPrimaryKeys** se comporta da seguinte forma:  
  
-   Ignora os argumentos *szTableOwner* e *cbTableOwner.*  
  
-   Funciona apenas para fontes de dados que são [bancos de dados](../../odbc/microsoft/visual-foxpro-terminology.md). O driver retorna o erro "O driver não suporta essa função" se a fonte de dados for um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obter mais informações, consulte [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) no *Programador ODBC*.
