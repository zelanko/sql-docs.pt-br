---
title: Conectando-se diretamente a Drivers | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.prod_service: drivers
ms.service: 
ms.component: odbc
ms.reviewer: 
ms.suite: sql
ms.technology: drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
caps.latest.revision: "6"
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 4da4d454eddccae8f72a29d5903887ffec14842c
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="connecting-directly-to-drivers"></a>Conectando-se diretamente a Drivers
Conforme abordado na [escolhendo uma fonte de dados ou Driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md)anteriormente nesta seção, alguns aplicativos não quiser usar uma fonte de dados. Em vez disso, eles desejam se conectar diretamente a um driver. **SQLDriverConnect** fornece uma maneira para que o aplicativo se conectar diretamente a um driver sem especificar uma fonte de dados. Conceitualmente, uma fonte de dados temporário é criada em tempo de execução.  
  
 Para se conectar diretamente a um driver, o aplicativo especifica o **DRIVER** palavra-chave na cadeia de conexão em vez do **DSN** palavra-chave. O valor de **DRIVER** palavra-chave é a descrição do driver como retornado por **SQLDrivers**. Por exemplo, suponha que um driver com a descrição do Driver Paradox e requer o nome de um diretório que contém os arquivos de dados. Para se conectar a este driver, o aplicativo pode usar qualquer uma das seguintes cadeias de caracteres de conexão:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Com a primeira cadeia de caracteres, o driver não precisaria informações adicionais. Com a segunda cadeia de caracteres, o driver necessário solicitar o nome do diretório que contém os arquivos de dados.
