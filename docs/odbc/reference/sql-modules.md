---
title: "Os módulos SQL | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: f37ab932ef230d29a5db23aec920230de0443e37
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="sql-modules"></a>Módulos do SQL
A segunda técnica para enviar instruções SQL para o DBMS é por meio de módulos. Em resumo, um módulo consiste em um grupo de procedimentos que são chamados de host de linguagem de programação. Cada procedimento contém uma única instrução SQL e dados são passados de e para o procedimento por meio de parâmetros.  
  
 Um módulo pode ser pensado como uma biblioteca de objeto que está vinculada ao código do aplicativo. No entanto, exatamente como os procedimentos e o restante do aplicativo são vinculados são dependentes de implementação. Por exemplo, os procedimentos podem ser compilados em código de objeto e vinculados diretamente para o código do aplicativo, pode ser compilados e armazenados no DBMS e chamadas para acessar os identificadores de plano colocados no código do aplicativo ou eles podem ser interpretados em tempo de execução.  
  
 A principal vantagem dos módulos é que eles corretamente separam instruções SQL de linguagem de programação. Em teoria, deve ser possível alterar um sem alterar o outro e simplesmente vincular novamente-los.
