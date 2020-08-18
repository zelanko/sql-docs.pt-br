---
description: Suporte internacional (Driver ODBC do Visual FoxPro)
title: Suporte internacional (driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- double-byte character sets [ODBC]
- FoxPro ODBC driver [ODBC], international support
- DBCS [ODBC]
- international support [ODBC]
- sort order [ODBC]
- collating sequences [ODBC]
- Visual FoxPro ODBC driver [ODBC], international support
ms.assetid: cd3fab32-13f1-4a86-abc4-5e18667669fc
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 575eb2361b5869f924cf2b8e5721121182b684db
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88449458"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Suporte internacional (Driver ODBC do Visual FoxPro)
O driver ODBC do Microsoft Visual FoxPro oferece suporte a:  
  
-   DBCS (conjuntos de caracteres de byte duplo)  
  
-   Várias sequências de agrupamento  
  
 Uma sequência de agrupamento define a *ordem de classificação* dos dados armazenados em uma tabela ou banco de dado do Visual FoxPro. Por padrão, o driver é configurado para usar as sequências de agrupamento que dão suporte à versão de idioma do seu sistema operacional.  
  
 Para obter uma lista de sequências de agrupamento com suporte, consulte [set COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>localidade  
 O conjunto de informações que corresponde a um determinado idioma e país/região. Uma localidade indica configurações específicas, como separadores decimais, formatos de data e hora e ordem de classificação de caracteres.  
  
## <a name="sort-order"></a>ordem de classificação  
 As ordens de classificação incorporam as regras de classificação de diferentes *locais*, permitindo que você classifique os dados nesses idiomas corretamente. No Visual FoxPro, a ordem de classificação atual determina os resultados das comparações de expressão de caractere e a ordem na qual os registros aparecem em tabelas indexadas ou classificadas.
