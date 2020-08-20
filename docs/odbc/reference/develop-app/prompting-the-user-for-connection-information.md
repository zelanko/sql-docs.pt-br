---
description: Solicitar o usuário para informações de conexão
title: Solicitando informações de conexão ao usuário | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- connecting to data source [ODBC], SqlConnect
- connecting to driver [ODBC], prompting user for information
- connecting to driver [ODBC], SQLConnect
- connecting to driver [ODBC], SQLDriverConnect
- connecting to data source [ODBC], SqlDriverConnect
- SQLConnect function [ODBC], prompting user for connection information
- connecting to data source [ODBC], prompting user for information
- prompting user for connection information [ODBC]
- SQLDriverConnect function [ODBC], prompting user for connection information
ms.assetid: da98e9b9-a4ac-4a9d-bae6-e9252b1fe1e5
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: f52e0d120fb150fe58b850107847d7ef5df20e7c
ms.sourcegitcommit: e700497f962e4c2274df16d9e651059b42ff1a10
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/17/2020
ms.locfileid: "88465708"
---
# <a name="prompting-the-user-for-connection-information"></a>Solicitar o usuário para informações de conexão
Se o aplicativo usar o **SQLConnect** e precisar solicitar informações de conexão ao usuário, como um nome de usuário e senha, ele deverá fazer isso por conta própria. Embora isso permita que o aplicativo controle sua "aparência", ele pode forçar o aplicativo a conter código específico do driver. Isso ocorre quando o aplicativo precisa solicitar informações de conexão específicas do driver ao usuário. Isso apresenta uma situação impossível para aplicativos genéricos, que são projetados para trabalhar com qualquer e todos os drivers, incluindo drivers que não existem quando o aplicativo é gravado.  
  
 **SQLDriverConnect** pode solicitar informações de conexão ao usuário. Por exemplo, o programa personalizado mencionado anteriormente poderia passar a seguinte cadeia de conexão para **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 O driver pode exibir uma caixa de diálogo solicitando IDs de usuário e senhas, semelhante à ilustração a seguir.  
  
 ![Caixa de diálogo que solicita IDs e senhas do usuário](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 O driver pode solicitar informações de conexão é particularmente útil para aplicativos genéricos e verticais. Esses aplicativos não devem conter informações específicas do driver e ter o prompt do driver para as informações necessárias mantém essas informações fora do aplicativo. Isso é mostrado pelos dois exemplos anteriores. Quando o aplicativo passasse apenas o nome da fonte de dados para o driver, o aplicativo não continha nenhuma informação específica do driver e, portanto, não estava vinculado a um driver específico. Quando o aplicativo passa uma cadeia de conexão completa para o driver, ele estava vinculado ao driver que poderia interpretar essa cadeia de caracteres.  
  
 Um aplicativo genérico pode levar isso um pouco além e nem mesmo especificar uma fonte de dados. Quando **SQLDriverConnect** recebe uma cadeia de conexão vazia, o Gerenciador de driver exibe a caixa de diálogo a seguir.  
  
 ![Caixa de diálogo Selecionar Fonte de Dados](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Depois que o usuário seleciona uma fonte de dados, o Gerenciador de driver constrói uma cadeia de conexão especificando essa fonte de dados e a passa para o driver. O driver pode solicitar ao usuário as informações adicionais necessárias.  
  
 As condições sob as quais o driver solicita o usuário são controladas pelo sinalizador *DriverCompletion* ; Há opções para sempre solicitar, avisar se necessário ou nunca avisar. Para obter uma descrição completa desse sinalizador, consulte a descrição da função [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) .
