---
title: Tipos de dados e comportamento de carregamento em massa de XML (SQLXML)
description: Saiba mais sobre os tipos de dados e o comportamento de carregamento em massa de XML no SQLXML 4,0.
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
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
ms.custom: seo-lt-2019
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: e77e4ca789a2abf5bb664221adb8911dd5a1bae5
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84529722"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os tipos de dados que são especificados no esquema de mapeamento (tipo XSD ou XDR e **SQL: DataType**) são geralmente ignorados, exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo for **DateTime** ou **time**, você deverá especificar o **SQL: DataType** porque o carregamento em massa de XML executa a conversão de dados antes de enviar os dados para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Quando você está carregando em massa em uma coluna de tipo **uniqueidentifier** em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: datatype = "uniqueidentifier"** para remover as chaves antes que o valor seja inserido na coluna. Se **SQL: DataType** não for especificado, o valor será enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações sobre **SQL: DataType**, consulte [coerção de tipo de dados e a anotação sql: datatype &#40;SQLXML 4,0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o **dt: Type** for **DateTime**, **time**, **DateTime.TZ**ou **time.TZ**, você deverá especificar os tipos de dados **dt: Type** e **SQL: DataType** porque o carregamento em massa de XML executa a conversão de dados antes de enviar os dados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] .  
  
-   Se os dados XML forem do tipo **UUID**, **SQL: DataType** deverá ser especificado; **dt: Type = "UUID"** também é necessário, a menos que os dados sejam dados de cadeia de caracteres. Se você não especificar **dt: UUID**, o carregamento em massa XML aceitará cadeias de caracteres com chaves (e as removerá se necessário).  
  
-   Se os dados XML forem **bin. base64** ou **bin. Hex**, você deverá especificar o tipo de dados XML com **dt: Type**. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
