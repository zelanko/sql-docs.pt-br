---
title: SQLBindCol (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLBindCol function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: 984d6605-39ba-4d33-ac94-22625bfa6107
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 1e5eda58c6dec31206de9ddb10e73bdf90272d0a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300636"
---
# <a name="sqlbindcol-visual-foxpro-odbc-driver"></a>SQLBindCol (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível de núcleo  
  
 Atribui espaço de armazenamento para uma coluna de resultado e especifica o tipo do resultado. Quando [SQLFetch](../../odbc/microsoft/sqlfetch-visual-foxpro-odbc-driver.md) ou [SQLExtendedFetch](../../odbc/microsoft/sqlextendedfetch-visual-foxpro-odbc-driver.md) é chamado, o driver coloca os dados de todas as colunas associadas nos locais atribuídos. Consulte [SQLGetTypeInfo](../../odbc/microsoft/sqlgettypeinfo-visual-foxpro-odbc-driver.md) para o mapeamento entre os tipos de dados ODBC e Visual FoxPro.  
  
 Para obter mais informações, consulte [SQLBindCol](../../odbc/reference/syntax/sqlbindcol-function.md) na *referência do programador de ODBC*.
