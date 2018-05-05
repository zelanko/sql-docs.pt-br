---
title: Avisar o usuário para obter informações de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.suite: sql
ms.technology: connectivity
ms.tgt_pltfrm: ''
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
caps.latest.revision: 7
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 305d8bf4c3e18fdb610c6b67b7c678c43e83c6f0
ms.sourcegitcommit: 1740f3090b168c0e809611a7aa6fd514075616bf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="prompting-the-user-for-connection-information"></a>Avisar o usuário para obter informações de Conexão
Se o aplicativo usa **SQLConnect** e precisa solicitar ao usuário informações de conexão, como um nome de usuário e senha, ele deve fazer isso em si. Enquanto isso permite que o aplicativo controlar seu "aparência", ele pode forçar o aplicativo para conter código específico do driver. Isso ocorre quando o aplicativo deve solicitar ao usuário informações de conexão específicas do driver. Isso apresenta uma situação impossível para aplicativos genéricos, que são projetados para trabalhar com todos os drivers, incluindo drivers que não existem quando o aplicativo é escrito.  
  
 **SQLDriverConnect** pode solicitar ao usuário informações de conexão. Por exemplo, o programa personalizado mencionado anteriormente poderia passar a seguinte cadeia de conexão para **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 O driver, em seguida, pode exibir uma caixa de diálogo que solicita IDs de usuário e senhas, semelhantes à ilustração a seguir.  
  
 ![Caixa de diálogo que solicita IDs de usuário e senhas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Se o driver pode solicitar informações de conexão é particularmente útil para aplicativos genéricos e verticais. Esses aplicativos não devem conter informações específicas de driver e ter o prompt de driver para as informações necessárias mantém informações do aplicativo. Isso é mostrado por dois exemplos anteriores. Quando o aplicativo transmitido apenas o nome da fonte de dados para o driver, o aplicativo não contém todas as informações específicas de driver e, portanto, não foi associado a um driver específico. Quando o aplicativo passada uma cadeia de caracteres de conexão completa para o driver, ele foi ligado ao driver que pode interpretar a cadeia de caracteres.  
  
 Um aplicativo genérico pode levar isso um passo adicional e especifique nem mesmo uma fonte de dados. Quando **SQLDriverConnect** recebe uma cadeia de caracteres de conexão vazia, o Gerenciador de Driver exibe a caixa de diálogo a seguir.  
  
 ![Caixa de diálogo Selecionar fonte de dados](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Depois que o usuário seleciona uma fonte de dados, o Gerenciador de Driver constrói uma cadeia de caracteres de conexão especificando essa fonte de dados e passa para o driver. O driver pode pedir ao usuário informações adicionais necessárias.  
  
 As condições sob as quais o driver solicita ao usuário são controladas pelo *DriverCompletion* sinalizador; há opções para sempre solicitar, solicitar se necessário ou nunca perguntar. Para obter uma descrição completa desse sinalizador, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.
