---
title: Tipos de dados e XML em massa o comportamento de carregamento (SQLXML 4.0) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.component: sqlxml
ms.reviewer: ''
ms.suite: sql
ms.technology: xml
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
monikerRange: = azuresqldb-current || >= sql-server-2016 || = sqlallproducts-allversions
ms.openlocfilehash: eb6f8a64d48e6fa1336a4f56ca63b07873ee7168
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="data-types-and-xml-bulk-load-behavior-sqlxml-40"></a>Tipos de dados e o comportamento do Carregamento em Massa de XML (SQLXML 4.0)
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]
  Os tipos de dados que são especificados no esquema de mapeamento (tipo XSD ou XDR e **SQL: DataType**) geralmente são ignoradas, exceto nos seguintes casos:  
  
 Em XSD:  
  
-   Se o tipo é **dateTime** ou **tempo**, você deve especificar o **SQL: DataType** porque o carregamento em massa XML realiza a conversão de dados antes de enviar os dados para a Microsoft [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Quando você está carregando em massa em uma coluna de **uniqueidentifier** digite [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] e o valor XSD é um GUID que inclui chaves ({e}), você deve especificar **SQL: DataType = "uniqueidentifier"** para Remova as chaves antes do valor é inserido na coluna. Se **SQL: DataType** não for especificado, o valor é enviado com as chaves e a inserção falhará.  
  
 Para obter mais informações sobre **SQL: DataType**, consulte [coerções de tipo de dados e a anotação SQL: DataType &#40;SQLXML 4.0&#41;](../../../relational-databases/sqlxml-annotated-xsd-schemas-using/data-type-coercions-and-the-sql-datatype-annotation-sqlxml-4-0.md).  
  
 Em XDR:  
  
-   Se o **dt: Type** é **datetime**, **tempo**, **dateTime.tz**, ou **time.tz**, você deve especificar ambos o **dt: Type** e **SQL: DataType** tipos de dados porque o carregamento em massa XML realiza a conversão de dados antes de enviar os dados a serem [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)].  
  
-   Se os dados XML são do tipo **uuid**, **SQL: DataType** deve ser especificado; **dt: type = "uuid"** também é necessária, a menos que os dados são dados de cadeia de caracteres. Se você não especificar **dt:uuid**, carregamento em massa XML aceitará cadeias com chaves (e remove-las se necessário).  
  
-   Se os dados XML são **bin.base64** ou **bin.hex**, você deve especificar o tipo de dados XML com **dt: Type**. O Carregamento em Massa XML carrega os dados no [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] como uma representação hexadecimal dos dados.  
  
  
