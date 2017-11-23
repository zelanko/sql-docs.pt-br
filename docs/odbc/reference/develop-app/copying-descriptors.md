---
title: Copiando descritores | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: "5"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 04ce43d9cc30012e559b27839b308f31b1617d35
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="copying-descriptors"></a>Descritores de cópias
O **SQLCopyDesc** função é chamada para copiar os campos do descritor de um descritor de outro. Campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de qualquer tipo de descritor. Somente os campos que são definidos para descritores de origem e destino são copiados. **SQLCopyDesc** não copia o campo SQL_DESC_ALLOC_TYPE, porque o tipo de alocação do descritor não pode ser alterado. Campos copiados substituem os campos existentes.  
  
 Um descartar no identificador de uma instrução pode servir como APD no outro identificador de instrução. Isso permite que um aplicativo para copiar linhas entre tabelas sem copiar os dados no nível do aplicativo. Para fazer isso, um descritor de linha que descreve uma linha de busca de uma tabela é reutilizado como um descritor de parâmetro para um parâmetro em uma instrução INSERT. O tipo de informação SQL_MAX_CONCURRENT_ACTIVITIES deve ser maior que 1 para essa operação seja bem-sucedida.
