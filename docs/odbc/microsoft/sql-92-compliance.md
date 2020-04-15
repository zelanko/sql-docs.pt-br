---
title: Conformidade SQL-92 | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300696"
---
# <a name="sql-92-compliance"></a>Conformidade com SQL-92
Os drivers de banco de dados de desktop oDBC e o mecanismo Microsoft Jet subjacente não são compatíveis com SQL-92. Eles suportam muitos recursos que foram definidos no SQL-92. Alguns recursos suportados no driver não são suportados no SQL-92. Para obter mais informações, consulte o *Guia do Programador do Motor do Banco de Dados microsoft jet*. A seguir, as principais diferenças entre os dois:  
  
-   O SQL usado pelos Drivers de banco de dados de desktop suporta expressões mais poderosas do que as especificadas pelo SQL-92.  
  
-   Regras diferentes se aplicam ao predicado BETWEEN.  
  
-   O SQL usado pelos Drivers de banco de dados de desktop e pelo ANSI SQL suporta diferentes palavras-chave.  
  
 Os seguintes recursos do SQL-92 não são suportados pelo Microsoft Jet SQL:  
  
-   Declarações de segurança, como GRANT e LOCK.  
  
-   DISTINTO com referências de função agregadas.  
  
 Os seguintes recursos são aprimoramentos no SQL usado pelos Drivers de banco de dados de desktop que não são especificados pelo SQL-92:  
  
-   A declaração TRANSFORM fornece suporte para consultas de guia cruzada.  
  
-   Funções agregadas adicionais **(StDev** e **VarP).**  
  
> [!NOTE]  
>  Os drivers de banco de dados de desktop suportam a sintaxe ANSI padrão para % (por cento) e _ (sublinhado), não * (asterisco) e ? (ponto de interrogação).
