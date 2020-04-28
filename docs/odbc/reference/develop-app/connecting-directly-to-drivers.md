---
title: Conectando-se diretamente aos drivers | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLDriverConnect function [ODBC], connecting directly to drivers
- connecting to driver [ODBC], drivers
ms.assetid: f86e198f-a088-4401-9106-aa62a0eb8f6e
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: d6aacb5d3df985949e04cdd47a9fe460cddbde6a
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "81299076"
---
# <a name="connecting-directly-to-drivers"></a>Conectar-se diretamente a drivers
Como foi discutido na [escolha de uma fonte de dados ou driver](../../../odbc/reference/develop-app/choosing-a-data-source-or-driver.md), anteriormente nesta seção, alguns aplicativos não desejam usar uma fonte de dados. Em vez disso, eles querem se conectar diretamente a um driver. O **SQLDriverConnect** fornece uma maneira para o aplicativo se conectar diretamente a um driver sem especificar uma fonte de dados. Conceitualmente, uma fonte de dados temporária é criada em tempo de execução.  
  
 Para se conectar diretamente a um driver, o aplicativo especifica a palavra-chave do **Driver** na cadeia de conexão em vez da palavra-chave **DSN** . O valor da palavra-chave do **Driver** é a descrição do driver, conforme retornado pelos **sqldrives**. Por exemplo, suponha que um driver tenha a descrição do driver do Paradox e exija o nome de um diretório que contém os arquivos de dados. Para se conectar a esse driver, o aplicativo pode usar qualquer uma das seguintes cadeias de conexão:  
  
```  
DRIVER={Paradox Driver};Directory=C:\PARADOX;  
DRIVER={Paradox Driver};  
```  
  
 Com a primeira cadeia de caracteres, o driver não precisaria de nenhuma informação adicional. Com a segunda cadeia de caracteres, o driver precisa solicitar o nome do diretório que contém os arquivos de dados.
