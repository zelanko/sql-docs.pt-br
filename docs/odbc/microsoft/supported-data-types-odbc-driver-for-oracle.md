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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 313254a3a117984d666d7c7be7e506386ae34e3b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81301111"
---
# <a name="supported-data-types-odbc-driver-for-oracle"></a>Tipos de dados com suporte (Driver ODBC para Oracle)
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 O ODBC driver for Oracle dá suporte a todos os tipos de dados do Oracle 7,3; no entanto, ele não dá suporte a nenhum dos novos tipos de dados Oracle8 listados aqui.  
  
|Tipo de dados|Oracle 7,3|Oracle8|  
|---------------|----------------|-------------|  
|BFILE|n/d|Sem suporte|  
|BLOB|n/d|Sem suporte|  
|CHAR|Com suporte|Com suporte|  
|CLOB|n/d|Sem suporte|  
|DATE|Com suporte|Com suporte|  
|FLOAT|Com suporte|Com suporte|  
|INTEGER|Com suporte|Com suporte|  
|LONG|Com suporte|Com suporte|  
|LONG RAW|Com suporte|Com suporte|  
|NCHAR|n/d|Sem suporte|  
|NCLOB|n/d|Sem suporte|  
|NUMBER|Com suporte|Com suporte|  
|NVARCHAR2|n/d|Sem suporte|  
|RAW|Com suporte|Com suporte|  
|VARCHAR2|Com suporte|Com suporte|  
|MLSLABEL|Sem suporte.|Sem suporte.|  
  
> [!NOTE]  
>  Para obter mais informações sobre o tamanho permitido da coluna VARCHAR, consulte [varchar Column size](../../odbc/microsoft/varchar-column-size-odbc-driver-for-oracle.md) neste guia.
