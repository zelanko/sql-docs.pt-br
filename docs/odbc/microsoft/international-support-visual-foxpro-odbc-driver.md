---
title: Suporte Internacional (Visual FoxPro ODBC Driver) | Microsoft Docs
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
ms.openlocfilehash: b4b0c758bb478ea6a468e6756c3d6f0f52c766f5
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299966"
---
# <a name="international-support-visual-foxpro-odbc-driver"></a>Suporte internacional (Driver ODBC do Visual FoxPro)
O driver Microsoft Visual FoxPro ODBC suporta:  
  
-   Conjuntos de caracteres de byte duplo (DBCS)  
  
-   Múltiplas seqüências de colisão  
  
 Uma seqüência de colisão define a *ordem de classificação* para dados armazenados em uma tabela ou banco de dados Visual FoxPro. Por padrão, o driver está configurado para usar as seqüências de colisão que suportam a versão de idioma do seu sistema operacional.  
  
 Para obter uma lista de seqüências de colagem suportadas, consulte [SET COLLATE](../../odbc/microsoft/set-collate-command.md).  
  
## <a name="locale"></a>localidade  
 O conjunto de informações que corresponde a um determinado idioma e país/região. Um local indica configurações específicas, como separadores decimais, formatos de data e hora e ordem de classificação de caracteres.  
  
## <a name="sort-order"></a>ordem de classificação  
 As ordens de classificação incorporam as regras de classificação de *diferentes locais,* permitindo classificar os dados nesses idiomas corretamente. No Visual FoxPro, a ordem de classificação atual determina os resultados das comparações de expressão de caracteres e a ordem em que os registros aparecem em tabelas indexadas ou classificadas.
