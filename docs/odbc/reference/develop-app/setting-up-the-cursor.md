---
title: Configurando o Cursor | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: reference
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- scrollable cursors [ODBC]
- cursors [ODBC], scrollable
- cursors [ODBC], creating
ms.assetid: b80afb0e-ef2f-408f-86f5-a392edd99a56
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 6687f1c38b5c7d653aaf2e3fe12d2e2e44bf31dc
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="setting-up-the-cursor"></a>Configurando o Cursor
O aplicativo pode especificar o tipo de cursor antes de executar uma instrução que cria um resultado definido. Ele faz isso com o atributo SQL_ATTR_CURSOR_TYPE de instrução. Se o aplicativo não especificar explicitamente um tipo, será usado um cursor somente de avanço. Para obter um cursor misto, um aplicativo especifica um cursor controlado por mas declara um conjunto de chaves tamanho menor que o conjunto de resultados tamanho.  
  
 Para cursores controlados por conjunto de chaves e mistos, o aplicativo também pode especificar o tamanho do conjunto de chaves. Ele faz isso com o atributo de instrução SQL_ATTR_KEYSET_SIZE. Se o tamanho do conjunto de chaves é definido como 0, o que é o padrão, o tamanho do conjunto de chaves é definido como o tamanho do conjunto de resultados e um cursor controlado por conjunto de chaves é usado. O tamanho do conjunto de chaves pode ser alterado após o cursor foi aberto.  
  
 O aplicativo também pode definir o tamanho do conjunto de linhas. Para obter mais informações, consulte [usando cursores em bloco](../../../odbc/reference/develop-app/using-block-cursors.md)anteriormente nesta seção.
