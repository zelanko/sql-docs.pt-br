---
title: Limitações de nomes de coluna | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 41d973afdac360af114da41620997cad23a2c740
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81281376"
---
# <a name="column-name-limitations"></a>Limitações de nome de coluna
Os nomes das colunas podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes da coluna contiverem caracteres, exceto letras, números e sublinhados, o nome deve ser delimitado, anexando-o entre aspas (').  
  
 Quando o driver Microsoft Access ou Microsoft Excel é usado, os nomes das colunas são limitados a 64 caracteres, e nomes mais longos geram um erro. Quando o driver Paradox é usado, o nome máximo da coluna é 25 caracteres. Quando o driver texto é usado, o nome máximo da coluna é 64 caracteres e nomes mais longos são truncados.  
  
 Quando o driver dBASE é usado, caracteres com um valor ASCII maior que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Excel é usado, se os nomes das colunas estiverem presentes, eles devem estar na primeira linha. Um nome que no Microsoft Excel usaria o caractere "!" deve ser incluído nas aspas traseiras ('). O caractere "!" é convertido para o caractere "$", porque o caractere "!" não é legal em um nome ODBC, mesmo quando o nome é incluído entre aspas. Todos os outros caracteres válidos do Microsoft Excel (exceto o caractere pipe (&#124;)) podem ser usados em um nome de coluna, incluindo espaços. Um identificador delimitado deve ser usado para um nome de coluna do Microsoft Excel para incluir um espaço. Nomes de coluna não especificados serão substituídos por nomes gerados pelo driver, por exemplo, "Col1" para a primeira coluna.  
  
 O caractere pipe (&#124;) não pode ser usado em um nome de coluna, quer o nome esteja incluído entre aspas traseiras ou não.  
  
 Quando o driver texto é usado, o driver fornece um nome padrão se um nome de coluna não for especificado. Por exemplo, o piloto chama a primeira coluna de F1, a segunda coluna F2, e assim por diante.
