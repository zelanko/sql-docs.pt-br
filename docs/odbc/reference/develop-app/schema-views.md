---
description: Exibições do esquema
title: Exibições de esquema | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 34e1b52b5e96b5fedb964e53f14a7b554d12aa05
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88429068"
---
# <a name="schema-views"></a>Exibições do esquema
Um aplicativo pode recuperar informações de metadados do DBMS chamando funções de catálogo ODBC ou usando exibições de INFORMATION_SCHEMA. As exibições são definidas pelo padrão ANSI SQL-92.  
  
 Se houver suporte do DBMS e do driver, as exibições de INFORMATION_SCHEMA fornecerão um meio mais poderoso e abrangente de recuperação de metadados do que as funções de catálogo ODBC fornecidas. Um aplicativo pode executar sua própria instrução **Select** personalizada em uma dessas exibições, pode unir exibições ou pode executar uma União em exibições. Ao mesmo tempo em que oferece um melhor utilitário e uma maior variedade de metadados, os modos de exibição de INFORMATION_SCHEMA geralmente não são suportados pelo DBMS. Isso pode mudar à medida que mais DBMSs e drivers atingirem a conformidade com o SQL-92.  
  
 Para determinar quais exibições têm suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_INFO_SCHEMA_VIEWS. Para recuperar metadados de uma exibição com suporte, o aplicativo executa uma instrução **Select** que especifica as informações de esquema necessárias.
