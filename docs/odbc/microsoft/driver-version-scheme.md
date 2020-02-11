---
title: Esquema de versão do driver | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
author: MightyPen
ms.author: genemi
ms.openlocfilehash: d8a155f5d76e8a250c64d3d59e160fbb5863414f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "68071852"
---
# <a name="driver-version-scheme"></a>Esquema de versão do driver
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista todas as versões lançadas do Microsoft ODBC driver for Oracle.  
  
|Versão do driver|Número de build|Histórico de disponibilidade|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4,2 e Visual Basic 5,0, Enterprise Edition|  
|2.0|2.73.7269|Visual Studio 97 e MDAC 1.5 a|  
|2,0 atualizado|2.73.7283.01|IIS 4,0|  
|2,0 atualizado|2.73.7283.03|MDAC 1.5 b e 1.5 c|  
|2,0 atualizado|2.73.7356|SDK DO ODBC 3,5|  
|2.5|2.573.2927|Visual Studio 6,0 e MDAC 2,0|  
|2,5 atualizado|2.573.3513|SQL Server 7,0<br /><br /> SQL Server 6,5 SP5|  
  
 O Build 2.00.6235 (versão 1) foi a primeira versão do Microsoft ODBC driver for Oracle. Após o lançamento da primeira versão, uma nova Convenção de nomenclatura foi adotada.  
  
 Por exemplo, 2.73.7283.03 pode ser dividido nos seguintes componentes distintos:  
  
-   2 = o número de versão.  
  
-   73 = a versão do servidor Oracle para a qual o driver foi projetado.  
  
-   7283, 3 = o número de Build do driver.  
  
> [!NOTE]  
>  Com a versão 2.573.2973, a Convenção de nomenclatura levou a alguma confusão de que 2,573 é uma versão anterior à 2,73, mas cada seção do número de Build deve ser considerada individualmente. O número 573 é maior que 73, portanto, é uma versão mais recente. Além disso, "2,5" indica o número de versão do driver.
