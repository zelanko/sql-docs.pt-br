---
title: Gerar um esquema XDR embutido | Microsoft Docs
description: Veja informações de como gerar um esquema XDR embutida e sobre a reprovação da diretiva XMLDATA na cláusula FOR XML.
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: xml
ms.topic: conceptual
helpviewer_keywords:
- XDR schemas [SQL Server]
- inline XDR schema generation [SQL Server]
- XMLDATA option
- FOR XML clause, inline XDR schema generation
ms.assetid: 2a40d617-9724-4f7d-80a4-a85c702f14d0
author: MightyPen
ms.author: genemi
ms.openlocfilehash: e61aeda134c63c8e9827c521b34be5fa839a259f
ms.sourcegitcommit: da88320c474c1c9124574f90d549c50ee3387b4c
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/01/2020
ms.locfileid: "85729880"
---
# <a name="generate-an-inline-xdr-schema"></a>Gerar um esquema XDR embutido
[!INCLUDE [SQL Server Azure SQL Database](../../includes/applies-to-version/sql-asdb.md)]
  A diretiva **XMLDATA** no FOR XML retorna um esquema XDR embutido junto com o resultado da consulta. No entanto, o esquema XDR não oferece suporte a todos os novos tipos de dados e outras melhorias apresentadas no [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)] e versões anteriores. Em vez disso, é possível solicitar um esquema XSD embutido usando [a diretiva XMLSCHEMA](../../relational-databases/xml/generate-an-inline-xsd-schema.md).  
  
> [!IMPORTANT]  
>  A diretiva XMLDATA para a opção FOR XML foi preterida. Use geração de XSD no caso dos modos RAW e AUTO. Não há substituição para a diretiva XMLDATA no modo EXPLICIT. [!INCLUDE[ssNoteDepFutureAvoid](../../includes/ssnotedepfutureavoid-md.md)]  
  
 Também observe o seguinte sobre o suporte ao esquema XDR:  
  
-   Se o resultado da consulta FOR XML incluir colunas de tipo **xml** e você solicitar um esquema XDR embutido, será retornado um erro. O XDR embutido não oferece suporte a esses tipos.  
  
-   Os tipos **(n)varchar(max)** e **(n)varbinary(max)** serão mapeados para **(n)varchar(n)** e **varbinary(n)** , respectivamente.  
  
-   Quando o modo de compatibilidade é definido como 90 ou superior, os valores **timestamp** são considerados como dados **varbinary(8)** , são tratados como dados binários e retornados no resultado da seguinte maneira:  
  
    -   A codificação de Base 64 é usada quando **binary base64** é especificado.  
  
    -   A codificação de URL é usada no modo AUTO quando **binary base64** não é especificado.  
  
  
