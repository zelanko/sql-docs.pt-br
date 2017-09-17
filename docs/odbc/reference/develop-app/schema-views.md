---
title: "Modos de exibição de esquema | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- schema views [ODBC]
- functions [ODBC], catalog functions
- catalog functions [ODBC], schema views
ms.assetid: f1dfb3e8-a7bd-46c3-92b6-c19531e8409d
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 06b9546950d5ae84b6ac5811ae4413fa1841c065
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="schema-views"></a>Exibições do esquema
Um aplicativo pode recuperar informações de metadados do DBMS chamando funções de catálogo ODBC ou por meio de exibições INFORMATION_SCHEMA. As exibições são definidas pelo padrão ANSI SQL-92.  
  
 Se o DBMS e suporte de driver, as exibições INFORMATION_SCHEMA fornecem um meio de mais poderoso e abrangente de recuperação de metadados que fornecem as funções de catálogo ODBC. Um aplicativo pode executar seu próprio personalizado **selecione** instrução em relação a um desses modos de exibição, pode unir as exibições, ou pode executar uma união em modos de exibição. Ao oferecer maior do utilitário e uma maior variedade de metadados, exibições INFORMATION_SCHEMA não têm suporte com frequência pelo DBMS. Isso pode ser alterado conforme mais DBMSs e drivers de alcançar a conformidade com o SQL-92.  
  
 Para determinar quais modos de exibição têm suporte, um aplicativo chama **SQLGetInfo** com a opção SQL_INFO_SCHEMA_VIEWS. Para recuperar metadados de um modo de exibição com suporte, o aplicativo executa um **selecione** instrução que especifica as informações de esquema necessárias.
