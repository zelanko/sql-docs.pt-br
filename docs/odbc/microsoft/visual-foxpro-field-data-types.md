---
title: Tipos de dados de campo do Visual FoxPro | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- field data types [ODBC]
- Visual FoxPro ODBC driver [ODBC], data types
ms.assetid: 50b733dc-679a-4b10-bc5d-98bb474dead2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 72313e0269c93bca9cb2561d89604c3c88c8567b
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81304797"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de dados de campo do Visual FoxPro
A tabela a seguir lista os valores para o argumento *FieldType* em alter table e CREATE TABLE e indica se os argumentos *nFieldWidth* e *nPrecision* são necessários.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|Descrição|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|Double|  
|C|N|-|Campo de caractere da largura *n*|  
|D|-|-|Data|  
|F|N|d|Campo numérico flutuante de largura *n* com casas decimais *d*|  
|G|-|-|Geral|  
|I|-|-|Integer|  
|L|-|-|Lógico|  
|M|-|-|Memo|  
|N|N|d|Campo numérico de largura *n* com casas decimais *d*|  
|T|-|-|Datetime|  
|S|-|-|Currency|
