---
title: Configurando o Cursor | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 59ade343f282933e05619996b119bc08e2dfb2ab
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47825514"
---
# <a name="setting-up-the-cursor"></a>Configurar o cursor
O aplicativo pode especificar o tipo de cursor antes de executar uma instrução que cria um resultado definido. Ele faz isso com o atributo SQL_ATTR_CURSOR_TYPE de instrução. Se o aplicativo não especificar explicitamente um tipo, um cursor somente de encaminhamento será usado. Para obter um cursor misto, um aplicativo especifica um cursor controlado por conjunto de chaves, mas declara um conjunto de chaves tamanho menor que o conjunto de resultados tamanho.  
  
 Para cursores controlados por e mistos, o aplicativo também pode especificar o tamanho do conjunto de chaves. Ele faz isso com o atributo de instrução SQL_ATTR_KEYSET_SIZE. Se o tamanho do conjunto de chaves é definido como 0, o que é o padrão, o tamanho do conjunto de chaves é definido como o tamanho do conjunto de resultados e um cursor controlado por conjunto de chaves é usado. O tamanho do conjunto de chaves pode ser alterado após o cursor foi aberto.  
  
 O aplicativo também pode definir o tamanho do conjunto de linhas. Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md), anteriormente nesta seção.
