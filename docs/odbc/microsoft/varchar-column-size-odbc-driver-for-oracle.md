---
title: Tamanho da coluna VARCHAR (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: db2871324f92ef6d84a8bf8313db105489100a96
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47847564"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamanho de coluna VARCHAR (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 No Oracle8, o tamanho máximo de uma coluna VARCHAR aumentou de 2000 a 4000 bytes. O software de cliente Oracle 7.3.x não tem nenhuma maneira de associar um valor de parâmetro maior que 2.000 bytes. Portanto, se você criar uma tabela com uma coluna VARCHAR do maior que 2000 bytes, não será possível executar consultas em relação a ela com os dados que excedem o limite de bytes de 2000 do software cliente, atualizações, exclusões e inserções com parâmetros. Como tanto o Driver ODBC para Oracle e o provedor OLE DB para Oracle usam consultas, atualizações, exclusões e inserções com parâmetros, eles relatará erros ORA 01026 nesse caso. Dados que esteja dentro dos limites impostos pelo software cliente Oracle funcionará. Para evitar esse limite de bytes de 2000, você deve atualizar o software cliente para Oracle8 (8.0.4.1.1c ou superior).
