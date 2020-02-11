---
title: Tamanho da coluna VARCHAR (driver ODBC para Oracle) | Microsoft Docs
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
ms.openlocfilehash: 3a3156c3f71eb4b3f7b8319da5d5fec7514f08b6
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087961"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamanho de coluna VARCHAR (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Em Oracle8, o tamanho máximo de uma coluna VARCHAR aumentou de 2000 para 4000 bytes. O software cliente Oracle 7.3. x não tem como associar um valor de parâmetro maior que 2000 bytes. Portanto, se você criar uma tabela com uma coluna VARCHAR maior que 2000 bytes, não será possível executar inserções, atualizações, exclusões e consultas parametrizadas com dados que excedem o limite de 2000 bytes do software cliente. Como o driver ODBC para Oracle e o provedor de OLE DB para Oracle usam inserções, atualizações, exclusões e consultas com parâmetros, eles relatarão erros de ORA-01026 nesse caso. Os dados que estão dentro dos limites impostos pelo software cliente Oracle funcionarão. Para evitar esse limite de 2000 bytes, você deve atualizar o software cliente para Oracle8 (8.0.4.1.1 c ou superior).
