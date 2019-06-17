---
title: Gateway padrão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC [ODBC], database access
- SQL [ODBC], database access
- database access [ODBC]
- standardizing database access [ODBC], gateways
- standard gateways [ODBC]
- gateways [ODBC]
ms.assetid: b8341492-2141-4bab-80bd-f2752223079e
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c70a558b065765dd9f8c0895345959e8aa22ebfe
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63232089"
---
# <a name="standard-gateway"></a>Gateway padrão
Um *gateway* é uma parte do software que faz com que um DBMS para se parecer com o outro. Ou seja, o gateway aceita a interface de programação, a gramática SQL e o protocolo de um DBMS único de fluxo de dados e converte-o para a interface de programação, gramática SQL, e protocolo do DBMS oculto de fluxo de dados. Por exemplo, aplicativos escritos para usar o Microsoft® SQL Server™ também podem acessar dados do DB2 por meio do Gateway Micro Decisionware DB2; Este produto faz com que o DB2 para se parecer com o SQL Server. Quando os gateways são usados, um gateway diferente deve ser escrito para cada banco de dados de destino.  
  
 Embora os gateways estão limitados pelas diferenças de arquitetura entre DBMSs, eles são um bom candidato para padronização. No entanto, se todos os DBMSs devem padronizar a interface de programação, gramática SQL e dados de fluxo de protocolo de um DBMS único cujo DBMS deve ser escolhido como o padrão? Certamente nenhum fornecedor do DBMS comercial provavelmente concorda com a padronizar em um produto de um concorrente. E se uma interface de programação padrão, a gramática SQL e o protocolo de fluxo de dados são desenvolvidos, nenhum gateway é necessária.
