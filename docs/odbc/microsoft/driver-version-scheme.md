---
title: "Esquema de versão de driver | Microsoft Docs"
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: microsoft
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords: ODBC driver for Oracle [ODBC], versions
ms.assetid: e4a8d9d7-8aba-48ab-8be6-1a6129adfb8f
caps.latest.revision: "8"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 35ee21329cabca4e160112887f8c746ad8f44b82
ms.sourcegitcommit: 7f8aebc72e7d0c8cff3990865c9f1316996a67d5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/20/2017
---
# <a name="driver-version-scheme"></a>Esquema de versão de driver
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista todas as versões do Driver de ODBC da Microsoft para Oracle.  
  
|Versão do driver|Número da compilação|Histórico de disponibilidade|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 e 5.0, Enterprise Edition do Visual Basic|  
|2.0|2.73.7269|Visual Studio 97 e MDAC 1.5|  
|2.0 atualizado|2.73.7283.01|IIS 4.0|  
|2.0 atualizado|2.73.7283.03|MDAC 1.5b e 1.5 c|  
|2.0 atualizado|2.73.7356|O ODBC 3.5 SDK|  
|2.5|2.573.2927|O Visual Studio 6.0 e o MDAC 2.0|  
|2.5 atualizado|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Compilação 2.00.6235 (versão 1) foi a primeira versão do Driver de ODBC da Microsoft para Oracle. Após o lançamento da primeira versão, uma convenção de nomenclatura novo foi adotada.  
  
 Por exemplo, 2.73.7283.03 pode ser dividido nos seguintes componentes distintos:  
  
-   2 = o número de versão.  
  
-   73 = a versão do servidor Oracle para o qual o driver foi criado.  
  
-   7283.03 = o número de compilação do driver.  
  
> [!NOTE]  
>  Com a versão 2.573.2973, a convenção de nomenclatura levou a alguma confusão que 2.573 é uma versão anterior que 2,73, mas cada seção do número de compilação deve ser considerada individualmente. O número 573 é maior que 73, portanto, é uma versão mais recente. Além disso, "2.5" indica o número de versão do driver.
