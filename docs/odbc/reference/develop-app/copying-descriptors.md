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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 2e2e5897afc3673a21396e256df04d25008c8cdf
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301665"
---
# <a name="copying-descriptors"></a>Copiar descritores
A função **SQLCopyDesc** é chamada para copiar os campos de um descritor para outro descritor. Os campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de qualquer tipo de descritor. Somente os campos que são definidos para os descritores de origem e de destino são copiados. **SQLCopyDesc** não copia o campo SQL_DESC_ALLOC_TYPE, porque o tipo de alocação de um descritor não pode ser alterado. Os campos copiados substituem os campos existentes.  
  
 Um ARD em um identificador de instrução pode servir como APD em outro identificador de instrução. Isso permite que um aplicativo Copie linhas entre tabelas sem copiar dados no nível do aplicativo. Para fazer isso, um descritor de linha que descreve uma linha buscada de uma tabela é reutilizado como um descritor de parâmetro para um parâmetro em uma instrução INSERT. O tipo de informação SQL_MAX_CONCURRENT_ACTIVITIES deve ser maior que 1 para que essa operação tenha sucesso.
