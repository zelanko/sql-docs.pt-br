---
title: Gateway padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: drivers
ms.service: ''
ms.component: odbc
ms.reviewer: ''
ms.suite: sql
ms.technology:
- drivers
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
caps.latest.revision: 5
author: MightyPen
ms.author: genemi
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ef59162739835fa2e6bdd0cba6bb4f4c648901cb
ms.sourcegitcommit: 7a6df3fd5bea9282ecdeffa94d13ea1da6def80a
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/16/2018
---
# <a name="standard-gateway"></a>Gateway padrão
Um *gateway* é um software que faz com que um DBMS para se parecer com o outro. Ou seja, o gateway aceita a interface de programação, a gramática SQL e dados de fluxo de protocolo de um único DBMS e converte-o para a interface de programação, gramática SQL, e protocolo do DBMS oculto. Por exemplo, aplicativos escritos para usar o Microsoft® SQL Server™ também podem acessar dados do DB2 por meio do Gateway de DB2 Micro Decisionware; Este produto faz com que o DB2 para se parecer com o SQL Server. Quando os gateways são usados, um gateway diferente deve ser escrito para cada banco de dados de destino.  
  
 Embora os gateways estão limitados pelas diferenças de arquitetura entre DBMSs, eles são um bom candidato para padronização. No entanto, se todos os DBMSs padronizar a interface de programação, gramática de SQL e dados de fluxo de protocolo de um único DBMS, cujo DBMS é escolhido como o padrão? Certamente nenhum fornecedor DBMS comercial é provavelmente concorda padronizar os produtos. E se uma interface de programação padrão, a gramática de SQL e o protocolo de fluxo de dados são desenvolvidos, nenhum gateway é necessária.
