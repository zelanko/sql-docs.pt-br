---
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
ms.openlocfilehash: 9ac0ae5873e545afb8fcac9dd003c984b1ed303a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81300696"
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
