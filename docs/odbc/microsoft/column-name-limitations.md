---
title: Limitações de nome de coluna | Microsoft Docs
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
- desktop database drivers [ODBC], column names
- ODBC desktop database drivers [ODBC], column names
ms.assetid: 5a339f61-c52f-40ad-8deb-d785f72753d4
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 3f3f384b9a2080ab683c8148effe7c6a9a13fcd6
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32899181"
---
# <a name="column-name-limitations"></a>Limitações de nome de coluna
Nomes de coluna podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de coluna contiverem qualquer caractere, exceto letras, números e sublinhados, o nome deve ser delimitado colocando-o entre aspas back (').  
  
 Quando o driver do Microsoft Access ou o Microsoft Excel é usado, os nomes de coluna são limitados a 64 caracteres e nomes mais geram um erro. Quando o driver do Paradox é usado, o nome de coluna máximo é 25 caracteres. Quando o driver de texto é usado, o nome de coluna máximo é 64 caracteres e nomes mais longos são truncados.  
  
 Quando o driver dBASE é usado, os caracteres com um valor ASCII maior do que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Excel é usado, se houver nomes de coluna, eles devem ser a primeira linha. Um nome que deseja usar no Microsoft Excel a "!" caractere deve ser colocado entre aspas back ('). O "!" caractere é convertido para o caractere "$", porque o "!" caractere não é válido em um nome ODBC, mesmo quando o nome é colocado entre aspas voltar. Todos os outros caracteres válidos do Microsoft Excel (exceto o caractere de pipe (&#124;)) pode ser usado em um nome de coluna, incluindo espaços. Um identificador delimitado deve ser usado para um nome de coluna do Microsoft Excel com um espaço. Nomes de coluna especificado serão substituídos com nomes gerados pelo driver, por exemplo, "Col1" para a primeira coluna.  
  
 O caractere de pipe (&#124;) não pode ser usado em um nome de coluna, se o nome é colocado entre aspas back ou não.  
  
 Quando o driver de texto é usado, o driver fornece um nome padrão, se não for especificado um nome de coluna. Por exemplo, o driver chama a primeira coluna F1, a segunda coluna F2 e assim por diante.
