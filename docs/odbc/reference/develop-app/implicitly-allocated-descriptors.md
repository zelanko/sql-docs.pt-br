---
description: Descritores implicitamente alocados
title: Descritores implicitamente alocados | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 5daa7f622798e1394c186b333069933b48e367af
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88461418"
---
# <a name="implicitly-allocated-descriptors"></a>Descritores implicitamente alocados
Quando um identificador de instrução é alocado, o aplicativo aloca implicitamente um conjunto de quatro descritores. O aplicativo pode obter os identificadores desses descritores implicitamente alocados como atributos do identificador de instrução. Quando o aplicativo libera o identificador de instrução, o driver libera todos os descritores implicitamente alocados nesse identificador.
