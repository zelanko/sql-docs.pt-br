---
title: Tipos de dados e XML em massa (SQLXML 4.0) de comportamento de carregamento | Microsoft Docs
ms.custom: ''
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
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 820d2b083544542d1c1414f978105fe992b0ce36
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67915156"
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os tipos de dados que são especificados no esquema de mapeamento (tipo XSD ou XDR e **SQL: DataType**) geralmente são ignoradas, exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo for **dateTime** ou **tempo**, você deve especificar o **SQL: DataType** pois carregamento em massa XML realiza a conversão de dados antes de enviar os dados para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando você estiver carregando em massa em uma coluna de **uniqueidentifier** digitar [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: DataType = "uniqueidentifier"** para Remova as chaves antes do valor é inserido na coluna. Se **SQL: DataType** não for especificado, o valor é enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações sobre **SQL: DataType**, consulte [coerções de tipo de dados e a anotação SQL: DataType &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o **dt: Type** é **datetime**, **tempo**, **dateTime.tz**, ou **time.tz**, você deve especificar ambos o **dt: Type** e **SQL: DataType** tipos de dados porque o carregamento em massa XML realiza a conversão de dados antes de enviar os dados a serem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se seus dados XML são do tipo **uuid**, **SQL: DataType** deve ser especificado; **dt: type = "uuid"** também é necessária, a menos que os dados são dados de cadeia de caracteres. Se você não especificar **dt:uuid**, carregamento em massa XML aceitará cadeias com chaves (e remove-las se necessário).  
  
-   Se os dados XML forem **bin.base64** ou **Hex**, você deve especificar o tipo de dados XML com **dt: Type**. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
