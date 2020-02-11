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
ms.openlocfilehash: 1b5cef56cec30e5ad09500135e05884bf55d5dde
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68076221"
---
# <a name="sql-modules"></a>Módulos SQL
A segunda técnica para enviar instruções SQL para o DBMS é por meio de módulos. Resumidamente, um módulo consiste em um grupo de procedimentos, que são chamados da linguagem de programação de host. Cada procedimento contém uma única instrução SQL e os dados são passados para e do procedimento por meio de parâmetros.  
  
 Um módulo pode ser considerado como uma biblioteca de objetos vinculada ao código do aplicativo. No entanto, exatamente como os procedimentos e o restante do aplicativo estão vinculados é dependente de implementação. Por exemplo, os procedimentos podem ser compilados no código de objeto e vinculados diretamente ao código do aplicativo, eles poderiam ser compilados e armazenados no DBMS e chamadas para acessar os identificadores de plano colocados no código do aplicativo ou podem ser interpretados em tempo de execução.  
  
 A principal vantagem dos módulos é que eles separam claramente as instruções SQL da linguagem de programação. Teoricamente, deve ser possível alterar um sem alterar o outro e simplesmente revinculá-los.
