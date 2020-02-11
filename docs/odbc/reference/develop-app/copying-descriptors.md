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
ms.openlocfilehash: 7d41cd744d39113c556c4ee8bc17411b7992e596
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68002144"
---
# <a name="copying-descriptors"></a>Copiar descritores
A função **SQLCopyDesc** é chamada para copiar os campos de um descritor para outro descritor. Os campos podem ser copiados somente para um descritor de aplicativo ou um IPD, mas não para um IRD. Os campos podem ser copiados de qualquer tipo de descritor. Somente os campos que são definidos para os descritores de origem e de destino são copiados. **SQLCopyDesc** não copia o campo SQL_DESC_ALLOC_TYPE, porque o tipo de alocação de um descritor não pode ser alterado. Os campos copiados substituem os campos existentes.  
  
 Um ARD em um identificador de instrução pode servir como APD em outro identificador de instrução. Isso permite que um aplicativo Copie linhas entre tabelas sem copiar dados no nível do aplicativo. Para fazer isso, um descritor de linha que descreve uma linha buscada de uma tabela é reutilizado como um descritor de parâmetro para um parâmetro em uma instrução INSERT. O tipo de informação SQL_MAX_CONCURRENT_ACTIVITIES deve ser maior que 1 para que essa operação tenha sucesso.
