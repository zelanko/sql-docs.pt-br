---
title: Tamanho da coluna varchar (Driver ODBC para Oracle) | Microsoft Docs
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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f11e1de3171521c57c80beb207d33e67d26d3e33
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81304821"
---
# <a name="varchar-column-size-odbc-driver-for-oracle"></a>Tamanho de coluna VARCHAR (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 No Oracle8, o tamanho máximo de uma coluna VARCHAR aumentou de 2000 para 4000 bytes. O software cliente Oracle 7.3.x não tem como vincular um valor de parâmetro maior que 2000 bytes. Portanto, se você criar uma tabela com uma coluna VARCHAR de mais de 2000 bytes, você não poderá executar inserções parametrizadas, atualizações, exclusões e consultas contra ela com dados que excedam o limite de 2000 bytes do software cliente. Como tanto o Driver ODBC para Oracle quanto o Provedor OLE DB para Oracle usam inserções, atualizações, exclusões e consultas parametrizadas, eles relatarão erros ora-01026 neste caso. Os dados que estão dentro dos limites impostos pelo software cliente Oracle funcionarão. Para evitar esse limite de 2000 bytes, você deve atualizar seu software cliente para oracle8 (8.0.4.1.1c ou superior).
