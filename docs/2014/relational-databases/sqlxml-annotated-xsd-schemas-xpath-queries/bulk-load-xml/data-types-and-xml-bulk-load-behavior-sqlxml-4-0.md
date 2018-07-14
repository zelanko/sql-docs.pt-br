---
title: Tipos de dados e XML em massa (SQLXML 4.0) de comportamento de carregamento | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.tgt_pltfrm: ''
ms.topic: reference
helpviewer_keywords:
- bulk load [SQLXML], data types
- data types [SQLXML], XML Bulk Load
- XML Bulk Load [SQLXML], data types
ms.assetid: d1ac1939-1f6c-4398-b7a7-a79ca608a4f1
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: ce59362d28c4d65e32834fd965cf710f49edb501
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37274672"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
  Geralmente são ignorados os tipos de dados especificados no esquema de mapeamento (tipo XSD ou XDR e `sql:datatype`), exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo for `dateTime` ou `time`, você deverá especificar `sql:datatype` pois o Carregamento em Massa XML realiza a conversão de dados antes de enviar os dados para o Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando você estiver carregando em massa em uma coluna de `uniqueidentifier` digitar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: DataType = "uniqueidentifier"** para remover as chaves antes do valor é inserido na coluna. Se `sql:datatype` não for especificado, o valor será enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações sobre `sql:datatype`, consulte [coerções de tipo de dados e a anotação SQL: DataType &#40;SQLXML 4.0&#41;](../../sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o `dt:type` for `datetime`, `time`, `dateTime.tz`, ou `time.tz`, você deverá especificar os tipos de dados `dt:type` e `sql:datatype`, pois o Carregamento em Massa XML realiza a conversão dos dados antes de enviá-los ao [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se seus dados XML são do tipo `uuid`, `sql:datatype` deve ser especificado; **dt: type = "uuid"** também é necessária, a menos que os dados são dados de cadeia de caracteres. Se você não especificar `dt:uuid`, o Carregamento em Massa XML aceitará cadeias com chaves (e as removerá se necessário).  
  
-   Se os dados XML forem `bin.base64` ou `bin.hex`, você deverá especificar o tipo de dados XML com `dt:type`. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
