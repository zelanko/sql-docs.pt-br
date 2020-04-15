---
title: Vistas do esquema | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304247"
---
# <a name="schema-views"></a>Exibições do esquema
Um aplicativo pode recuperar informações de metadados do DBMS, ligando para funções de catálogo do ODBC ou usando INFORMATION_SCHEMA visualizações. As visualizações são definidas pela norma ANSI SQL-92.  
  
 Se apoiado pelo DBMS e pelo driver, as INFORMATION_SCHEMA visualizações fornecem um meio mais poderoso e abrangente de recuperar metadados do que as funções de catálogo do ODBC fornecem. Um aplicativo pode executar sua própria declaração **SELECT** personalizada contra uma dessas exibições, pode juntar visualizações ou executar uma união sobre visualizações. Embora ofereça maior utilidade e uma gama mais ampla de metadados, INFORMATION_SCHEMA visualizações não são frequentemente suportadas pelo DBMS. Isso pode mudar à medida que mais DBMSs e drivers atingem a conformidade com o SQL-92.  
  
 Para determinar quais visualizações são suportadas, um aplicativo chama **SQLGetInfo** com a opção SQL_INFO_SCHEMA_VIEWS. Para recuperar metadados de uma exibição suportada, o aplicativo executa uma declaração **SELECT** que especifica as informações de esquema necessárias.
