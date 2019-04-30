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
manager: craigg
ms.openlocfilehash: 8a80ed397ae494bc686ef76aaeeef10b61662f19
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63301805"
---
# <a name="column-name-limitations"></a>Limitações de nome de coluna
Nomes de coluna podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de coluna contiverem qualquer caractere, exceto letras, números e sublinhados, o nome deve ser delimitado, colocando-o no back-aspas (').  
  
 Quando o driver do Microsoft Access ou Microsoft Excel for usado, os nomes de coluna são limitados a 64 caracteres e nomes mais longos geram um erro. Quando o driver do Paradox é usado, o nome de coluna máximo for 25 caracteres. Quando o driver de texto é usado, o nome de coluna máximo é 64 caracteres e nomes mais longos são truncados.  
  
 Quando o driver do dBASE é usado, os caracteres com um valor de ASCII maior do que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Excel é usado, se houver nomes de coluna, eles devem ser na primeira linha. Um nome que deseja usar no Microsoft Excel a "!" caractere deve ser colocado entre aspas back ('). O "!" caractere é convertido para o caractere "$", porque o "!" caractere não é legal em um nome ODBC, mesmo quando o nome é colocado entre aspas back. Todos os outros caracteres válidos do Microsoft Excel (exceto o caractere de barra vertical (&#124;)) pode ser usado em um nome de coluna, incluindo espaços. Um identificador delimitado deve ser usado para um nome de coluna do Microsoft Excel para incluir um espaço. Nomes de coluna não especificado serão substituídos com nomes gerados pelo driver, por exemplo, "Col1" para a primeira coluna.  
  
 O caractere de barra vertical (&#124;) não pode ser usado em um nome de coluna, se o nome é colocado entre aspas voltar ou não.  
  
 Quando o driver de texto é usado, o driver fornece um nome padrão, se não for especificado um nome de coluna. Por exemplo, o driver chama a primeira coluna F1, a segunda coluna F2 e assim por diante.
