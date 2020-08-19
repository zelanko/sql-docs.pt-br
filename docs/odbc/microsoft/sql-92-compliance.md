---
description: Conformidade com SQL-92
title: Conformidade com SQL-92 | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- Jet-based ODBC drivers [ODBC], SQL-92 compliance
- desktop database drivers [ODBC], SQL-92 compliance
- SQL-92 compliance [ODBC]
- ODBC desktop database drivers [ODBC], SQL-92 compliance
ms.assetid: 50c8c7df-df01-4f4d-ad62-d059cf29d73a
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 7d978b236c45d442732cd3602c3fbbb6d16dfd8f
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88483429"
---
# <a name="sql-92-compliance"></a>Conformidade com SQL-92
Os drivers de banco de dados da área de trabalho ODBC e o mecanismo do Microsoft Jet subjacente não são compatíveis com SQL-92. Eles dão suporte a muitos recursos que foram definidos no SQL-92. Alguns recursos com suporte no driver não têm suporte no SQL-92. Para obter mais informações, consulte o *Guia do programador do Microsoft Jet mecanismo de banco de dados*. A seguir estão as principais diferenças entre as duas:  
  
-   O SQL usado pelos drivers de banco de dados de desktop dá suporte a expressões mais poderosas do que aquelas especificadas pelo SQL-92.  
  
-   Regras diferentes se aplicam ao predicado BETWEEN.  
  
-   O SQL usado pelos drivers de banco de dados da área de trabalho e ANSI SQL dá suporte a palavras-chave diferentes.  
  
 Os seguintes recursos do SQL-92 não têm suporte do Microsoft Jet SQL:  
  
-   Instruções de segurança, como GRANT e LOCK.  
  
-   DISTINCT com referências de função de agregação.  
  
 Os recursos a seguir são aprimoramentos no SQL usado pelos drivers de banco de dados da área de trabalho que não são especificados pelo SQL-92:  
  
-   A instrução TRANSFORM que fornece suporte para consultas de tabela de referência cruzada.  
  
-   Funções de agregação adicionais (**DESVPAD** e **VARP**).  
  
> [!NOTE]  
>  Os drivers de banco de dados de desktop dão suporte à sintaxe ANSI padrão para% (PERCENT) e _ (sublinhado), não * (asterisco) e? (ponto de interrogação).
