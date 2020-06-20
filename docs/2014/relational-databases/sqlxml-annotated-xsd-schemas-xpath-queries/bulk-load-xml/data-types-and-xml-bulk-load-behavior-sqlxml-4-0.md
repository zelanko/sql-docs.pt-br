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
author: rothja
ms.author: jroth
ms.openlocfilehash: 34b03423f3bb88166d0d9ce5b0df450d4455e7ef
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85068167"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
  Geralmente são ignorados os tipos de dados especificados no esquema de mapeamento (tipo XSD ou XDR e `sql:datatype`), exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo for `dateTime` ou `time`, você deverá especificar `sql:datatype` pois o Carregamento em Massa XML realiza a conversão de dados antes de enviar os dados para o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando você está carregando em massa em uma coluna do `uniqueidentifier` tipo in [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: datatype = "uniqueidentifier"** para remover as chaves antes que o valor seja inserido na coluna. Se `sql:datatype` não for especificado, o valor será enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações sobre `sql:datatype` , consulte [coerção de tipo de dados e a anotação sql: DataType &#40;SQLXML 4,0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o `dt:type` for `datetime`, `time`, `dateTime.tz`, ou `time.tz`, você deverá especificar os tipos de dados `dt:type` e `sql:datatype`, pois o Carregamento em Massa XML realiza a conversão dos dados antes de enviá-los ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se os dados XML forem do tipo `uuid` , `sql:datatype` deverá ser especificado; **dt: Type = "UUID"** também é necessário, a menos que os dados sejam dados de cadeia de caracteres. Se você não especificar `dt:uuid`, o Carregamento em Massa XML aceitará cadeias com chaves (e as removerá se necessário).  
  
-   Se os dados XML forem `bin.base64` ou `bin.hex`, você deverá especificar o tipo de dados XML com `dt:type`. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
