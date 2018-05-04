---
title: Copiando descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], copying
- copying descriptors [ODBC]
ms.assetid: 949a860d-6579-4218-882e-8c061688dd87
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: b452725d7a8379dcd8f27228261af8b471d96b08
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="copying-descriptors"></a>Descritores de cópias
O **SQLCopyDesc** função é chamada para copiar os campos do descritor de um descritor de outro. Campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de qualquer tipo de descritor. Somente os campos que são definidos para descritores de origem e destino são copiados. **SQLCopyDesc** não copia o campo SQL_DESC_ALLOC_TYPE, porque o tipo de alocação do descritor não pode ser alterado. Campos copiados substituem os campos existentes.  
  
 Um descartar no identificador de uma instrução pode servir como APD no outro identificador de instrução. Isso permite que um aplicativo para copiar linhas entre tabelas sem copiar os dados no nível do aplicativo. Para fazer isso, um descritor de linha que descreve uma linha de busca de uma tabela é reutilizado como um descritor de parâmetro para um parâmetro em uma instrução INSERT. O tipo de informação SQL_MAX_CONCURRENT_ACTIVITIES deve ser maior que 1 para essa operação seja bem-sucedida.
