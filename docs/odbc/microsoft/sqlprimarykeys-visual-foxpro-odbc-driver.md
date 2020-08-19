---
description: SQLPrimaryKeys (Driver ODBC do Visual FoxPro)
title: SQLPrimaryKeys (driver ODBC do Visual FoxPro) | Microsoft Docs
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
ms.openlocfilehash: 96b333e10c7000a8a44e957e33d0c84a3b004f43
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483339"
---
# <a name="sqlprimarykeys-visual-foxpro-odbc-driver"></a>SQLPrimaryKeys (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 2  
  
 Retorna os nomes de coluna que compõem a chave primária de uma tabela. A implementação do driver ODBC do Visual FoxPro de **SQLPrimaryKeys** se comporta da seguinte maneira:  
  
-   Ignora os argumentos *szTableOwner* e *cbTableOwner* .  
  
-   Funciona somente para fontes de dados que são [bancos](../../odbc/microsoft/visual-foxpro-terminology.md)de dado. O driver retornará o erro "o driver não oferece suporte a essa função" se a fonte de dados for um diretório de [tabelas livres](../../odbc/microsoft/visual-foxpro-terminology.md).  
  
 Para obter mais informações, consulte [SQLPrimaryKeys](../../odbc/reference/syntax/sqlprimarykeys-function.md) na *referência do programador de ODBC*.
