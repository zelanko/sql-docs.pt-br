---
description: SQLSpecialColumns (Driver ODBC do Visual FoxPro)
title: SQLSpecialColumns (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQLSpecialColumns function [ODBC], Visual FoxPro ODBC Driver
ms.assetid: b72a978d-6a60-475a-b7d9-c424d77bbe30
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: e83568c8370b56decb7c3f7c90cda443b88a72a7
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88421600"
---
# <a name="sqlspecialcolumns-visual-foxpro-odbc-driver"></a>SQLSpecialColumns (Driver ODBC do Visual FoxPro)
> [!NOTE]  
>  Este tópico contém informações específicas do driver ODBC do Visual FoxPro. Para obter informações gerais sobre essa função, consulte o tópico apropriado em [referência da API do ODBC](../../odbc/reference/syntax/odbc-api-reference.md).  
  
 Suporte: completo  
  
 Conformidade da API ODBC: nível 1  
  
 Recupera o conjunto ideal de colunas que identifica exclusivamente uma linha na tabela.  
  
 O driver ODBC do Visual FoxPro retorna as colunas que compõem a chave primária na tabela do FoxPro. (Consulte [SQLPrimaryKeys](../../odbc/microsoft/sqlprimarykeys-visual-foxpro-odbc-driver.md).) Se chamado com *fColType* definido como SQL_ROWVER, nenhuma coluna será retornada. **SQLSpecialColumns** funciona apenas para fontes de dados que são [bancos](../../odbc/microsoft/visual-foxpro-terminology.md)de dado.  
  
 Para obter mais informações, consulte [SQLSpecialColumns](../../odbc/reference/syntax/sqlspecialcolumns-function.md) na *referência do programador de ODBC*.
