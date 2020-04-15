---
title: Limitações de nome da tabela | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81289212"
---
# <a name="table-name-limitations"></a>Limitações de nome de tabela
Os nomes das tabelas podem conter quaisquer caracteres válidos (por exemplo, espaços). Se os nomes das tabelas contiverem caracteres, exceto letras, números e sublinhados, o nome deve ser delimitado, envolvendo-o entre aspas (').  
  
 Quando o driver do Microsoft Excel é usado e um nome de tabela não é qualificado por uma referência de banco de dados, o banco de dados padrão está implícito. Se um nome no Microsoft Excel incluir o caractere "!", ele será automaticamente traduzido para o caractere "$".  
  
 O nome da tabela \<do Microsoft Excel que faz referência ao nome do arquivo> é suportado para arquivos Microsoft Excel 3.0 e 4.0. O nome da tabela \<do Microsoft Excel que faz referência ao nome da pasta de trabalho> é suportado para arquivos Microsoft Excel 5.0, 7.0 ou 97.  
  
 Quando o driver dBASE é usado, caracteres com um valor ASCII maior que 127 são convertidos em sublinhados.  
  
 Quando o driver microsoft access é usado, o nome da tabela é limitado a 64 caracteres.  
  
 Quando o driver dBASE, Microsoft Excel 3.0 ou 4.0, Paradox ou Text driver é usado, as palavras-chave especiais MS-DOS CON, AUX, LPT1 e LPT2 não devem ser usadas como nomes de tabela.
