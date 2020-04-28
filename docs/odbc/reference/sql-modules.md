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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 351d1c6a34413b385bd76dfebb009b34c4c0f150
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280417"
---
# <a name="sql-modules"></a>Módulos SQL
A segunda técnica para enviar instruções SQL para o DBMS é por meio de módulos. Resumidamente, um módulo consiste em um grupo de procedimentos, que são chamados da linguagem de programação de host. Cada procedimento contém uma única instrução SQL e os dados são passados para e do procedimento por meio de parâmetros.  
  
 Um módulo pode ser considerado como uma biblioteca de objetos vinculada ao código do aplicativo. No entanto, exatamente como os procedimentos e o restante do aplicativo estão vinculados é dependente de implementação. Por exemplo, os procedimentos podem ser compilados no código de objeto e vinculados diretamente ao código do aplicativo, eles poderiam ser compilados e armazenados no DBMS e chamadas para acessar os identificadores de plano colocados no código do aplicativo ou podem ser interpretados em tempo de execução.  
  
 A principal vantagem dos módulos é que eles separam claramente as instruções SQL da linguagem de programação. Teoricamente, deve ser possível alterar um sem alterar o outro e simplesmente revinculá-los.
