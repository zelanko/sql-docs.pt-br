---
title: Copiando descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: da22ba86ea49532f460b081b13e18d6b7d95211c
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042752"
---
# <a name="copying-descriptors"></a>Copiar descritores
O **SQLCopyDesc** função é chamada para copiar os campos de descritor de um descritor de outro. Campos podem ser copiados apenas a um descritor de aplicativo ou um IPD, mas não a um IRD. Campos podem ser copiados de qualquer tipo de descritor. Apenas os campos que são definidos para descritores de origem e destino são copiados. **SQLCopyDesc** não copia o campo SQL_DESC_ALLOC_TYPE, porque o tipo de alocação de um descritor não pode ser alterado. Campos copiados substituem os campos existentes.  
  
 Um descartar no identificador de uma instrução pode servir como APD no outro identificador de instrução. Isso permite que um aplicativo para copiar linhas entre tabelas sem copiar os dados no nível do aplicativo. Para fazer isso, um descritor de linha que descreve uma linha de busca de uma tabela é reutilizado como um descritor de parâmetro para um parâmetro em uma instrução INSERT. O tipo de informação SQL_MAX_CONCURRENT_ACTIVITIES deve ser maior que 1 para essa operação seja bem-sucedida.
