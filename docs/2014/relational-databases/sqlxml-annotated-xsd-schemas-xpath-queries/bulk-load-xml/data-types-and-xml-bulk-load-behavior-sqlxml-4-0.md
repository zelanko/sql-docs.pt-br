---
title: Tipos de dados e comportamento de carregamento em massa de XML (SQLXML 4,0) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: xml
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 2d2eb9af2b353760f5b195b95d6a9f9d5d1efc9b
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66013422"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
  Geralmente são ignorados os tipos de dados especificados no esquema de mapeamento (tipo XSD ou XDR e `sql:datatype`), exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo for `dateTime` ou `time`, você deverá especificar `sql:datatype` pois o Carregamento em Massa XML realiza a conversão de dados antes de enviar os dados para o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando você está carregando em massa em uma coluna `uniqueidentifier` do tipo [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] in e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: datatype = "uniqueidentifier"** para remover as chaves antes que o valor seja inserido na coluna. Se `sql:datatype` não for especificado, o valor será enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações `sql:datatype`sobre, consulte [coerção de tipo de dados e a anotação sql: datatype &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o `dt:type` for `datetime`, `time`, `dateTime.tz`, ou `time.tz`, você deverá especificar os tipos de dados `dt:type` e `sql:datatype`, pois o Carregamento em Massa XML realiza a conversão dos dados antes de enviá-los ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se os dados XML forem do tipo `uuid`, `sql:datatype` deverá ser especificado; **dt: Type = "UUID"** também é necessário, a menos que os dados sejam dados de cadeia de caracteres. Se você não especificar `dt:uuid`, o Carregamento em Massa XML aceitará cadeias com chaves (e as removerá se necessário).  
  
-   Se os dados XML forem `bin.base64` ou `bin.hex`, você deverá especificar o tipo de dados XML com `dt:type`. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
