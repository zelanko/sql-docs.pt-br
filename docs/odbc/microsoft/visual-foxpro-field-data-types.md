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
author: MightyPen
ms.author: genemi
ms.openlocfilehash: 217058bf328677bf375d346ae7201c6eb81efa4e
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68087952"
---
# <a name="visual-foxpro-field-data-types"></a>Tipos de dados de campo do Visual FoxPro
A tabela a seguir lista os valores para o argumento *FieldType* em alter table e CREATE TABLE e indica se os argumentos *nFieldWidth* e *nPrecision* são necessários.  
  
|*FieldType*|*NFieldWidth*|*nPrecision*|DESCRIÇÃO|  
|-----------------|-------------------|------------------|-----------------|  
|B|-|d|DOUBLE|  
|C|N|-|Campo de caractere da largura *n*|  
|D|-|-|Data|  
|F|N|d|Campo numérico flutuante de largura *n* com casas decimais *d*|  
|G|-|-|Geral|  
|I|-|-|Integer|  
|L|-|-|Lógico|  
|M|-|-|Campos|  
|N|N|d|Campo numérico de largura *n* com casas decimais *d*|  
|T|-|-|DateTime|  
|S|-|-|Moeda|
