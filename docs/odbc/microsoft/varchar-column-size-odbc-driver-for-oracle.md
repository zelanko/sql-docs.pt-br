---
title: Tamanho de coluna VARCHAR (Driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- varchar column size [ODBC]
- ODBC driver for Oracle [ODBC], data types
ms.assetid: eb4cb410-3d00-4251-8c5e-a06f36c4dac7
caps.latest.revision: 8
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 02e02b9faf3bd19665536e141884bd663ad64266
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamanho de coluna VARCHAR (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em Oracle8, o tamanho máximo de uma coluna VARCHAR aumentou de 2000 a 4000 bytes. O software de cliente Oracle 7.3.x tem uma forma de vincular um valor de parâmetro maior que 2.000 bytes. Portanto, se você criar uma tabela com uma coluna VARCHAR do maior do que 2.000 bytes, não será possível executar com parâmetros inserções, atualizações, exclusões e consultas em relação a ela com dados que excedem o limite de bytes de 2000 do software cliente. Tanto o Driver ODBC do Oracle e o provedor OLE DB para Oracle usar consultas, atualizações, exclusões e inserções com parâmetros, eles reportará ORA-01026 erros nesse caso. Dados que esteja dentro dos limites impostos pelo software cliente Oracle funcionará. Para evitar esse limite de bytes de 2000, você deve atualizar o software cliente para Oracle8 (8.0.4.1.1c ou superior).
