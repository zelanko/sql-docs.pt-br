---
title: Limitações da instrução ALTER TABLE | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC SQL grammar, ALTER TABLE statement limitations
- ALTER TABLE statement limitations [ODBC]
ms.assetid: f3e88f85-edf4-47cd-a822-292b106ddb34
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 1333cd6cd5946b7a3a70152e12f4d3decfa7fed0
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68138428"
---
# <a name="alter-table-statement-limitations"></a>Limitações da instrução ALTER TABLE
Quando o driver dBASE ou Paradox for usado, depois que um índice tiver sido criado e um novo registro for adicionado, a estrutura da tabela não poderá ser alterada pela instrução ALTER TABLE, a menos que o índice seja descartado e o conteúdo da tabela seja excluído.  
  
 Não há suporte para instruções ALTER TABLE para os drivers de texto ou do Microsoft Excel.  
  
> [!NOTE]  
>  Quando você usa o driver do Paradox sem implementar o Borland Mecanismo de Banco de Dados, não há suporte para instruções ALTER TABLE; somente instruções Read e Append são permitidas.
