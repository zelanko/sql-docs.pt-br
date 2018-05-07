---
title: Suporte internacional (Driver ODBC do Visual FoxPro) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 151d3989737d221e46f6771055d0775c69f7e576
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Suporte internacional (Driver ODBC do Visual FoxPro)
O Driver ODBC do Microsoft Visual FoxPro dá suporte a:  
  
-   Conjuntos de caracteres de dois bytes (DBCS)  
  
-   Várias sequências de agrupamento  
  
 A sequência de agrupamento define a *ordem de classificação* para dados armazenados em uma tabela do Visual FoxPro ou banco de dados. Por padrão, o driver está configurado para usar as sequências de agrupamento que oferecem suporte à versão do idioma de seu sistema operacional.  
  
 Para obter uma lista de sequências de agrupamento com suporte, consulte [definir COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>localidade  
 O conjunto de informações que corresponde a um determinado idioma e país/região. Uma localidade indica configurações específicas, como separadores decimais e ordem de classificação de caractere e formatos de hora e data.  
  
## <a name="sort-order"></a>ordem de classificação  
 Ordens de classificação incorporam as regras de classificação de diferentes *localidade*s, permitindo que você classifique os dados nesses idiomas corretamente. No Visual FoxPro, a ordem de classificação atual determina os resultados das comparações de expressão de caractere e a ordem na qual os registros aparecem no indexados ou classificados tabelas.
