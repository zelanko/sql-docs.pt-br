---
title: Limitações de nome de coluna | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 14e62555db2e88c6573f3bdca0d4a1a2733d428b
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68006243"
---
# <a name="column-name-limitations"></a>Limitações de nome de coluna
Os nomes de coluna podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de coluna contiverem caracteres, exceto letras, números e sublinhados, o nome deverá ser delimitado ao colocá-lo entre aspas (').  
  
 Quando o Microsoft Access ou o driver do Microsoft Excel é usado, os nomes de coluna são limitados a 64 caracteres e os nomes mais longos geram um erro. Quando o driver do Paradox for usado, o nome máximo da coluna será de 25 caracteres. Quando o driver de texto é usado, o nome máximo da coluna é de 64 caracteres e os nomes mais longos são truncados.  
  
 Quando o driver do dBASE é usado, os caracteres com um valor ASCII maior que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Excel for usado, se os nomes de coluna estiverem presentes, eles deverão estar na primeira linha. Um nome que no Microsoft Excel usaria o caractere "!" deve ser colocado entre aspas regressivas ('). O caractere "!" é convertido para o caractere "$", porque o caractere "!" não é válido em um nome ODBC, mesmo quando o nome é colocado entre aspas. Todos os outros caracteres válidos do Microsoft Excel (exceto o caractere de pipe (&#124;)) podem ser usados em um nome de coluna, incluindo espaços. Um identificador delimitado deve ser usado para um nome de coluna do Microsoft Excel para incluir um espaço. Os nomes de coluna não especificados serão substituídos por nomes gerados pelo driver, por exemplo, "Col1" para a primeira coluna.  
  
 O caractere de barra vertical (&#124;) não pode ser usado em um nome de coluna, independentemente de o nome ser colocado entre aspas de fundo ou não.  
  
 Quando o driver de texto for usado, o driver fornecerá um nome padrão se um nome de coluna não for especificado. Por exemplo, o driver chama a primeira coluna F1, a segunda coluna F2 e assim por diante.
