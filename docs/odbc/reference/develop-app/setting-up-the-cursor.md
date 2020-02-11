---
title: Configurando o cursor | Microsoft Docs
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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: c47e534f069f810948189f2668d4ecdfbfa4ad79
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68107541"
---
# <a name="setting-up-the-cursor"></a>Configurar o cursor
O aplicativo pode especificar o tipo de cursor antes de executar uma instrução que cria um conjunto de resultados. Ele faz isso com o atributo de instrução SQL_ATTR_CURSOR_TYPE. Se o aplicativo não especificar explicitamente um tipo, um cursor de somente avanço será usado. Para obter um cursor misto, um aplicativo especifica um cursor controlado por conjunto de chaves, mas declara um tamanho de conjunto de chaves menor do que o tamanho definido de resultado.  
  
 Para cursores mistos e controlados por conjunto de chaves, o aplicativo também pode especificar o tamanho do conjunto de chaves. Ele faz isso com o atributo de instrução SQL_ATTR_KEYSET_SIZE. Se o tamanho do conjunto de chaves for definido como 0, que é o padrão, o tamanho do conconjunto de chaves será definido como o tamanho da definição de resultado e um cursor controlado por conjuntos de chaves será usado. O tamanho do conjunto de chaves pode ser alterado após a abertura do cursor.  
  
 O aplicativo também pode definir o tamanho do conjunto de linhas; para obter mais informações, consulte [usando cursores de bloco](../../../odbc/reference/develop-app/using-block-cursors.md), anteriormente nesta seção.
