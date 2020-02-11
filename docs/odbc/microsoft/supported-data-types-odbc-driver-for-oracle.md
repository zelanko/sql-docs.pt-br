---
title: Tipos de dados com suporte (driver ODBC para Oracle) | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data types [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], data types
ms.assetid: 21d5f8d9-a3aa-4aa4-bc37-ff8bc90c0870
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 145170afee5ab791602695c662ce1e80e86cae7e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "67915677"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipos de dados com suporte (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O ODBC driver for Oracle dá suporte a todos os tipos de dados do Oracle 7,3; no entanto, ele não dá suporte a nenhum dos novos tipos de dados Oracle8 listados aqui.  
  
|Tipo de dados|Oracle 7,3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|Sem suporte|  
|BLOB|n/d|Sem suporte|  
|CHAR|Suportado|Suportado|  
|CLOB|n/d|Sem suporte|  
|DATE|Suportado|Suportado|  
|FLOAT|Suportado|Suportado|  
|INTEGER|Suportado|Suportado|  
|LONG|Suportado|Suportado|  
|LONG RAW|Suportado|Suportado|  
|NCHAR|n/d|Sem suporte|  
|NCLOB|n/d|Sem suporte|  
|NUMBER|Suportado|Suportado|  
|NVARCHAR2|n/d|Sem suporte|  
|RAW|Suportado|Suportado|  
|VARCHAR2|Suportado|Suportado|  
|MLSLABEL|Sem suporte.|Sem suporte.|  
  
> [!NOTE]  
>  Para obter mais informações sobre o tamanho permitido da coluna VARCHAR, consulte [varchar Column size](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
