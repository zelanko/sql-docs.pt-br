---
title: Limitações de nome de tabela | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, table name limitations
- table name limitations [ODBC]
- Excel driver [ODBC], table name limitations
ms.assetid: d9843e4b-1d05-4d5a-9dc3-ee9ec59edb97
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 738c563961eae56471f0238d9726a1ebb0bdc76e
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81289212"
---
# <a name="table-name-limitations"></a>Limitações de nome de tabela
Os nomes de tabela podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes de tabela contiverem caracteres, exceto letras, números e sublinhados, o nome deverá ser delimitado ao colocá-lo entre aspas (').  
  
 Quando o driver do Microsoft Excel é usado e um nome de tabela não é qualificado por uma referência de banco de dados, o banco de dados padrão é implícito. Se um nome no Microsoft Excel incluir o caractere "!", ele será automaticamente convertido para o caractere "$" em vez disso.  
  
 O nome da tabela do Microsoft Excel \<que faz referência ao nome de arquivo> tem suporte para arquivos do microsoft Excel 3,0 e 4,0. O nome da tabela do Microsoft Excel \<que faz referência ao nome da pasta de trabalho> tem suporte para arquivos do Microsoft Excel 5,0, 7,0 ou 97.  
  
 Quando o driver do dBASE é usado, os caracteres com um valor ASCII maior que 127 são convertidos em sublinhados.  
  
 Quando o driver do Microsoft Access é usado, o nome da tabela é limitado a 64 caracteres.  
  
 Quando o dBASE, o Microsoft Excel 3,0 ou o 4,0, o Paradox ou o driver de texto são usados, as palavras-chave do MS-DOS especiais CON, AUX, LPT1 e LPT2 não devem ser usadas como nomes de tabela.
