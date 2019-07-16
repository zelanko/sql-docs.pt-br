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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1e2dd512ab529f1fb5d216f4a2e459cd601d40e8
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67943753"
---
# <a name="schema-views"></a>Exibições do esquema
Um aplicativo pode recuperar informações de metadados do DBMS, chamando funções de catálogo ODBC ou por meio de exibições INFORMATION_SCHEMA. Os modos de exibição são definidos pelo padrão ANSI SQL-92.  
  
 Se compatível com o driver e o DBMS, as exibições INFORMATION_SCHEMA fornecem um meio de mais poderoso e abrangente de recuperação de metadados que fornecem funções de catálogo ODBC. Um aplicativo pode executar seu próprio custom **selecionar** instrução em relação a um desses modos de exibição, pode unir as exibições, ou pode executar uma união em modos de exibição. Oferecendo maior do utilitário e uma maior variedade de metadados, exibições INFORMATION_SCHEMA não têm suporte com frequência pelo DBMS. Isso pode mudar conforme mais drivers e DBMSs de alcançar a conformidade com o SQL-92.  
  
 Para determinar quais modos de exibição têm suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_INFO_SCHEMA_VIEWS. Para recuperar metadados de um modo de exibição com suporte, o aplicativo executa um **selecionar** declaração que especifica as informações de esquema necessárias.
