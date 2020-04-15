---
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
ms.openlocfilehash: 271d479a9d2faa8cd7ab01e02e830b194c4138b2
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81300126"
---
# <a name="implicitly-allocated-descriptors"></a>Descritores implicitamente alocados
Quando uma alça de declaração é alocada, o aplicativo aloca implicitamente um conjunto de quatro descritores. O aplicativo pode obter as alças desses descritores implicitamente alocados como atributos da alça da declaração. Quando o aplicativo libera a alça da declaração, o driver libera todos os descritores alocados implicitamente nessa alça.
