---
title: Avisar o usuário para obter informações de Conexão | Microsoft Docs
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
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: 58df84bf96306a2cfbc0567a3d5f6cb13514a06e
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62861885"
---
# <a name="prompting-the-user-for-connection-information"></a>Solicitar o usuário para informações de conexão
Se o aplicativo usa **SQLConnect** e precisa solicitar ao usuário as informações de conexão, como um nome de usuário e senha, deverá fazê-lo em si. Enquanto isso permite que o aplicativo controlar seu "aparência", isso poderá forçar o aplicativo contenha código específico do driver. Isso ocorre quando o aplicativo precisa solicitar ao usuário informações de conexão específicas do driver. Isso apresenta uma situação impossível para aplicativos genéricos, que são projetados para funcionar com todos os drivers, incluindo drivers que não existem quando o aplicativo é escrito.  
  
 **SQLDriverConnect** pode avisar o usuário para obter informações de conexão. Por exemplo, o programa personalizado, mencionado anteriormente poderia passar a seguinte cadeia de conexão para **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 O driver, em seguida, pode exibir uma caixa de diálogo que solicita IDs de usuário e senhas, semelhantes à ilustração a seguir.  
  
 ![Caixa de diálogo que solicita IDs de usuário e senhas](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Se o driver pode solicitar informações de conexão é particularmente útil para aplicativos genéricos e verticais. Esses aplicativos não devem conter informações específicas de driver e ter o prompt de driver para as informações necessárias mantém essas informações fora do aplicativo. Isso é mostrado por dois exemplos anteriores. Quando o aplicativo passou apenas o nome da fonte de dados para o driver, o aplicativo não contém quaisquer informações específicas de driver e, portanto, não associado a um driver específico. Quando o aplicativo passou uma cadeia de caracteres de conexão completa para o driver, ele foi vinculado ao driver que poderia interpretar essa cadeia de caracteres.  
  
 Um aplicativo genérico pode levar isso um passo além e nem mesmo especificar uma fonte de dados. Quando **SQLDriverConnect** recebe uma cadeia de caracteres de conexão vazia, o Gerenciador de Driver exibe a caixa de diálogo a seguir.  
  
 ![Marque a caixa de diálogo fonte de dados](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Depois que o usuário seleciona uma fonte de dados, o Gerenciador de Driver constrói uma cadeia de caracteres de conexão especificando essa fonte de dados e o passa para o driver. O driver, em seguida, pode avisar o usuário para todas as informações adicionais necessárias.  
  
 As condições sob as quais o driver solicita ao usuário que são controladas pelo *DriverCompletion* sinalizador; há opções para sempre solicitar, solicitará que, se necessário ou para nunca solicitar. Para obter uma descrição completa desse sinalizador, consulte o [SQLDriverConnect](../../../odbc/reference/syntax/sqldriverconnect-function.md) descrição da função.
