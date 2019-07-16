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
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68071852"
---
# <a name="driver-version-scheme"></a>Esquema de versão do driver
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista todas as versões do Driver Microsoft ODBC para Oracle.  
  
|Versão do driver|Número de build|Histórico de disponibilidade|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 e 5.0, Enterprise Edition do Visual Basic|  
|2.0|2.73.7269|Visual Studio 97 e o MDAC 1.5|  
|2.0 atualizado|2.73.7283.01|IIS 4.0|  
|2.0 atualizado|2.73.7283.03|MDAC 1.5b e 1.5 c|  
|2.0 atualizado|2.73.7356|O ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 e o MDAC 2.0|  
|2.5 atualizado|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Compilação 2.00.6235 (versão 1) foi a primeira versão do Driver Microsoft ODBC para Oracle. Após o lançamento da primeira versão, uma nova convenção de nomenclatura foi adotada.  
  
 Por exemplo, 2.73.7283.03 podem ser divididos nos seguintes componentes distintos:  
  
-   2 = o número de versão.  
  
-   73 = a versão do servidor Oracle para o qual o driver foi criado.  
  
-   7283.03 = o número de build do driver.  
  
> [!NOTE]  
>  Com a versão 2.573.2973, a convenção de nomenclatura levou a uma certa confusão que 2.573 é uma versão anterior que 2,73, mas cada seção do número de build deve ser considerada individualmente. O número 573 é maior do que 73, portanto, é uma versão mais recente. Além disso, "2.5" indica o número de versão do driver.
