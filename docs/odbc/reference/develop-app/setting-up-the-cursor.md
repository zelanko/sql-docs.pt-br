---
title: Configuração do Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 805d8076c853513d86f9a3a92d9342d1224226c9
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81299796"
---
# <a name="setting-up-the-cursor"></a>Configurar o cursor
O aplicativo pode especificar o tipo de cursor antes de executar uma declaração que cria um conjunto de resultados. Ele faz isso com o atributo de declaração SQL_ATTR_CURSOR_TYPE. Se o aplicativo não especificar explicitamente um tipo, um cursor somente para frente será usado. Para obter um cursor misto, um aplicativo especifica um cursor orientado por chave, mas declara um tamanho de conjunto de tecla menor do que o tamanho do conjunto de resultados.  
  
 Para cursores mistos e orientados por chaves, o aplicativo também pode especificar o tamanho do conjunto de chaves. Ele faz isso com o atributo de declaração SQL_ATTR_KEYSET_SIZE. Se o tamanho do conjunto de chaves estiver definido como 0, que é o padrão, o tamanho do conjunto de chaves será definido para o tamanho do conjunto de resultados e um cursor orientado por chaveé. O tamanho do conjunto de chaves pode ser alterado após a abertura do cursor.  
  
 O aplicativo também pode definir o tamanho do conjunto de linhas; para obter mais informações, consulte [Usando cursors de](../../../odbc/reference/develop-app/using-block-cursors.md)bloco, mais cedo nesta seção.
