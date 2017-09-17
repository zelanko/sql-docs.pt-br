---
title: "Selecione para instruções de atualização de processamento | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- ODBC cursor library [ODBC], statement processing
- SQL statements [ODBC], select for update statements
- select for update [ODBC]
- SQL statements [ODBC], cursor library
- cursor library [ODBC], select for update statements
- ODBC cursor library [ODBC], select for update statements
- cursor library [ODBC], statement processing
ms.assetid: 8d2e79a4-5daf-458e-a536-d8b6e588753e
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: ada17f95371246e3b43e1e9482ab9595f85a8db1
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="processing-select-for-update-statements"></a>Selecione para instruções de atualização de processamento
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. A Microsoft recomenda o uso da funcionalidade de cursor do driver.  
  
 Para interoperabilidade máxima, aplicativos devem gerar conjuntos de resultados serão atualizados com uma instrução update posicionadas executando um **Selecione para atualizar** instrução. Embora a biblioteca de cursores não exige isso, ele é necessário para a maioria das fontes de dados que oferecem suporte a instruções update posicionadas.  
  
 A biblioteca de cursores ignora as colunas a **para atualização** cláusula de um **SELECT FOR UPDATE** instrução; remove essa cláusula antes de passar a instrução para o driver. Na biblioteca de cursor, o atributo de instrução SQL_ATTR_CONCURRENCY, junto com as restrições mencionadas na seção anterior, controla se as colunas em um resultado de conjunto pode ser atualizada.
