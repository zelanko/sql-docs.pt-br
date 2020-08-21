---
title: Conectando-se ao SQLDriverConnect | Microsoft Docs
description: O SQLDriverConnect fornece funcionalidade de conexão adicional sobre o SQLConnect, incluindo opções para solicitar ao usuário mais informações.
ms.custom: ''
ms.date: 08/20/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- data sources [ODBC], connection functions
- functions [ODBC], data source or driver connections
- connecting to data source [ODBC], SQLDriverConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], functions
- connecting to driver [ODBC], functions
- SQLDriverConnect function [ODBC], connecting
- connection functions [ODBC]
- ODBC drivers [ODBC], connection functions
ms.assetid: e46e959f-d3c5-4ddb-810a-107bfcb83fd2
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: 78186e903405aa1b59cfac185e62646dbda6e77a
ms.sourcegitcommit: dc8a30a4a27e15fc6671ca2674da9b7c637ec255
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88746166"
---
# <a name="connecting-with-sqldriverconnect"></a>Conectar-se com o SQLDriverConnect

**SQLDriverConnect** é usado para se conectar a uma fonte de dados usando uma cadeia de conexão. **SQLDriverConnect** é usado em vez do **SQLConnect** para os seguintes cenários:  
  
- Estabeleça uma conexão usando uma cadeia de conexão que contenha o nome da fonte de dados, uma ou mais IDs de usuário, uma ou mais senhas e outras informações exigidas pela fonte de dados.  
  
- Estabelecer uma conexão usando uma cadeia de conexão parcial ou nenhuma informação adicional; Nesse caso, o Gerenciador de driver e o driver podem solicitar informações de conexão ao usuário.  
  
- Estabeleça uma conexão com uma fonte de dados que não esteja definida nas informações do sistema. Se o aplicativo fornecer uma cadeia de conexão parcial, o driver poderá solicitar informações de conexão ao usuário.  
  
- Estabeleça uma conexão com uma fonte de dados usando uma cadeia de conexão construída com as informações em um arquivo. DSN.  
  
Depois que uma conexão é estabelecida, **SQLDriverConnect** retorna a cadeia de conexão concluída. O aplicativo pode usar essa cadeia de caracteres para solicitações de conexão subsequentes.

Esta seção contém os seguintes tópicos.  
  
- [Informações de conexão específicas de driver](driver-specific-connection-information.md)  
  
- [Solicitar o usuário para informações de conexão](prompting-the-user-for-connection-information.md)  
  
- [Conectar-se usando fontes de dados de arquivo](connecting-using-file-data-sources.md)  
  
- [Conectar-se diretamente a drivers](connecting-directly-to-drivers.md)
