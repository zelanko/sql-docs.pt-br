---
title: Implicitamente alocados descritores | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- descriptors [ODBC], allocating and freeing
- implicitly allocated descriptors [ODBC]
- allocating and freeing descriptors [ODBC]
ms.assetid: 9f88c863-affc-4ab4-a558-63a3ef766f37
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: fa25e99c5bc0b0a5799cfac479e97bd9b89db338
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "62447230"
---
# <a name="implicitly-allocated-descriptors"></a>Descritores implicitamente alocados
Quando um identificador de instrução é alocado, o aplicativo aloca implicitamente um conjunto de descritores de quatro. O aplicativo pode obter os identificadores desses implicitamente alocados descritores como atributos do identificador de instrução. Quando o aplicativo libera o identificador de instrução, o driver libera todos os descritores implicitamente alocados nesse identificador.
