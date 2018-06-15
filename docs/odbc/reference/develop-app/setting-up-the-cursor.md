---
title: Configurando o Cursor | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: 6
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 9ae6f687a09658121955f1e1d8b258ae7233657e
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
ms.locfileid: "32912541"
---
# <a name="setting-up-the-cursor"></a>Configurando o Cursor
O aplicativo pode especificar o tipo de cursor antes de executar uma instrução que cria um resultado definido. Ele faz isso com o atributo SQL_ATTR_CURSOR_TYPE de instrução. Se o aplicativo não especificar explicitamente um tipo, será usado um cursor somente de avanço. Para obter um cursor misto, um aplicativo especifica um cursor controlado por mas declara um conjunto de chaves tamanho menor que o conjunto de resultados tamanho.  
  
 Para cursores controlados por conjunto de chaves e mistos, o aplicativo também pode especificar o tamanho do conjunto de chaves. Ele faz isso com o atributo de instrução SQL_ATTR_KEYSET_SIZE. Se o tamanho do conjunto de chaves é definido como 0, o que é o padrão, o tamanho do conjunto de chaves é definido como o tamanho do conjunto de resultados e um cursor controlado por conjunto de chaves é usado. O tamanho do conjunto de chaves pode ser alterado após o cursor foi aberto.  
  
 O aplicativo também pode definir o tamanho do conjunto de linhas. Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)anteriormente nesta seção.
