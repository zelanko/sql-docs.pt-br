---
title: Módulos SQL | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- SQL modules [ODBC]
- sending SQL statements to DBMS [ODBC]
- SQL [ODBC], modules
- modules [ODBC]
- SQL statements [ODBC], modules
ms.assetid: 07551472-87ee-4765-951f-1364ed32f0c0
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 30c116878049c4f6a8f36e988731ab641e03c6d7
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47834744"
---
# <a name="sql-modules"></a>Módulos SQL
A segunda técnica para enviar instruções SQL para o DBMS é por meio de módulos. Em resumo, um módulo consiste em um grupo de procedimentos, que são chamados do host de linguagem de programação. Cada procedimento contém uma única instrução SQL e dados são passados de e para o procedimento por meio de parâmetros.  
  
 Um módulo pode ser pensado como uma biblioteca de objetos que esteja vinculada ao código do aplicativo. No entanto, exatamente como os procedimentos e o restante do aplicativo são vinculados é dependente da implementação. Por exemplo, os procedimentos poderiam ser compilados em código de objeto e vinculados diretamente ao código do aplicativo, pode ser compilados e armazenados no DBMS e chamadas para acessar identificadores de plano colocados no código do aplicativo, ou eles puderam ser interpretados em tempo de execução.  
  
 A principal vantagem dos módulos é que eles corretamente separam instruções SQL de linguagem de programação. Em teoria, ele deve ser possível alterar um deles sem alterar o outro e simplesmente revinculá-los.
