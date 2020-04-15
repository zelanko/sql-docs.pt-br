---
title: Gateway Padrão | Microsoft Docs
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
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81280069"
---
# <a name="standard-gateway"></a>Gateway padrão
Um *gateway* é um software que faz com que um DBMS se pareça com outro. Ou seja, o gateway aceita a interface de programação, gramática SQL e protocolo de fluxo de dados de um único DBMS e o traduz para a interface de programação, gramática SQL e protocolo de fluxo de dados do DBMS oculto. Por exemplo, aplicativos escritos para usar o Microsoft® SQL Server™ também podem acessar dados DB2 através do Micro Decisionware DB2 Gateway; este produto faz com que o DB2 se pareça com o SQL Server. Quando os gateways são usados, um gateway diferente deve ser escrito para cada banco de dados de destino.  
  
 Embora os gateways sejam limitados por diferenças arquitetônicas entre os DBMSs, eles são um bom candidato à padronização. No entanto, se todos os DBMSs forem padronizar na interface de programação, gramática SQL e protocolo de fluxo de dados de um único DBMS, cujo DBMS deve ser escolhido como padrão? Certamente nenhum fornecedor comercial de DBMS provavelmente concordará em padronizar o produto de um concorrente. E se uma interface de programação padrão, gramática SQL e protocolo de fluxo de dados forem desenvolvidos, nenhum gateway será necessário.
