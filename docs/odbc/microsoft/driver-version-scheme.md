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
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 864a8bd892315b060fc6fcf42dbe69dfea61ae59
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81303447"
---
# <a name="driver-version-scheme"></a>Esquema de versão do driver
> [!IMPORTANT]  
>  Esse recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 A tabela a seguir lista todas as versões lançadas do Microsoft ODBC Driver for Oracle.  
  
|Versão do driver|Número de build|Histórico de disponibilidade|  
|--------------------|------------------|--------------------------|  
|1.0|2.00.6235|Visual C++ 4.2 e Visual Basic 5.0, Enterprise Edition|  
|2,0|2.73.7269|Visual Studio 97 e MDAC 1.5a|  
|2.0 atualizado|2.73.7283.01|IIS 4.0|  
|2.0 atualizado|2.73.7283.03|MDAC 1.5b e 1.5c|  
|2.0 atualizado|2.73.7356|ODBC 3.5 SDK|  
|2.5|2.573.2927|Visual Studio 6.0 e MDAC 2.0|  
|2.5 atualizado|2.573.3513|SQL Server 7.0<br /><br /> SQL Server 6.5 SP5|  
  
 Build 2.00.6235 (versão 1) foi o primeiro lançamento do Microsoft ODBC Driver para Oracle. Após o lançamento da primeira versão, uma nova convenção de nomeação foi adotada.  
  
 Por exemplo, 2.73.7283.03 pode ser dividido nos seguintes componentes distintos:  
  
-   2 = O número da versão.  
  
-   73 = A versão do Oracle Server para a qual o driver foi projetado.  
  
-   7283,03 = O número de construção do motorista.  
  
> [!NOTE]  
>  Com a liberação 2.573.2973, a convenção de nomeação levou a alguma confusão de que 2.573 é uma versão anterior de 2,73, mas cada seção do número de compilação deve ser considerada individualmente. O número 573 é maior que 73, por isso é uma versão mais recente. Além disso, "2.5" indica o número da versão do motorista.
