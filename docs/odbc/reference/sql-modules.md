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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280417"
---
# <a name="sql-modules"></a>Módulos SQL
A segunda técnica para enviar instruções SQL para o DBMS é através de módulos. Resumidamente, um módulo consiste em um grupo de procedimentos, que são chamados da linguagem de programação do host. Cada procedimento contém uma única declaração SQL, e os dados são passados para e a partir do procedimento através de parâmetros.  
  
 Um módulo pode ser pensado como uma biblioteca de objetos que está vinculada ao código do aplicativo. No entanto, exatamente como os procedimentos e o resto do aplicativo estão vinculados é dependente da implementação. Por exemplo, os procedimentos poderiam ser compilados em código de objeto e ligados diretamente ao código do aplicativo, eles poderiam ser compilados e armazenados no DBMS e chamadas para acessar identificadores de planos colocados no código do aplicativo, ou poderiam ser interpretados em tempo de execução.  
  
 A principal vantagem dos módulos é que eles separam limpamente as instruções SQL da linguagem de programação. Em teoria, deve ser possível mudar um sem mudar o outro e simplesmente revinculá-los.
