---
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
ms.openlocfilehash: a1a9e421c4835d35e3c4f3c644e69b8c7601e8e4
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304247"
---
# <a name="schema-views"></a>Exibições do esquema
Um aplicativo pode recuperar informações de metadados do DBMS chamando funções de catálogo ODBC ou usando exibições de INFORMATION_SCHEMA. As exibições são definidas pelo padrão ANSI SQL-92.  
  
 Se houver suporte do DBMS e do driver, as exibições de INFORMATION_SCHEMA fornecerão um meio mais poderoso e abrangente de recuperação de metadados do que as funções de catálogo ODBC fornecidas. Um aplicativo pode executar sua própria instrução **Select** personalizada em uma dessas exibições, pode unir exibições ou pode executar uma União em exibições. Ao mesmo tempo em que oferece um melhor utilitário e uma maior variedade de metadados, os modos de exibição de INFORMATION_SCHEMA geralmente não são suportados pelo DBMS. Isso pode mudar à medida que mais DBMSs e drivers atingirem a conformidade com o SQL-92.  
  
 Para determinar quais exibições têm suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_INFO_SCHEMA_VIEWS. Para recuperar metadados de uma exibição com suporte, o aplicativo executa uma instrução **Select** que especifica as informações de esquema necessárias.
