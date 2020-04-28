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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 67551845c0dd8c6a28c0c4bc1c50f54ee8232df1
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81280069"
---
# <a name="standard-gateway"></a>Gateway padrão
Um *Gateway* é uma parte do software que faz com que um DBMS se pareça com o outro. Ou seja, o gateway aceita a interface de programação, a gramática do SQL e o protocolo de fluxo de dados de um único DBMS e os converte para a interface de programação, a gramática do SQL e o protocolo de fluxo de dados do DBMS oculto. Por exemplo, os aplicativos escritos para usar o Microsoft® SQL Server™ também podem acessar dados do DB2 por meio do gateway do DB2 de tomada de decisões; Este produto faz com que o DB2 pareça SQL Server. Quando os gateways são usados, um gateway diferente deve ser gravado para cada banco de dados de destino.  
  
 Embora os gateways sejam limitados pelas diferenças de arquitetura entre DBMSs, eles são um bom candidato para padronização. No entanto, se todos os DBMSs forem padronizados na interface de programação, na gramática do SQL e no protocolo de fluxo de dados de um único DBMS, cujo DBMS deve ser escolhido como o padrão? Certamente, nenhum fornecedor de DBMS comercial provavelmente concorda em padronizar o produto de um concorrente. E se uma interface de programação padrão, uma gramática SQL e um protocolo de fluxo de dados forem desenvolvidos, nenhum gateway será necessário.
