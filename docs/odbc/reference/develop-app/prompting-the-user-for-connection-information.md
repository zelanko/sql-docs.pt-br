---
title: Solicitando informações ao Usuário sobre conexão | Microsoft Docs
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
ms.openlocfilehash: 9b0f120a1076f14f5e67d506e52a446e0a3d4713
ms.sourcegitcommit: ce94c2ad7a50945481172782c270b5b0206e61de
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/14/2020
ms.locfileid: "81282079"
---
# <a name="prompting-the-user-for-connection-information"></a>Solicitar o usuário para informações de conexão
Se o aplicativo usa **o SQLConnect** e precisa solicitar ao usuário qualquer informação de conexão, como nome de usuário e senha, ele deve fazê-lo sozinho. Embora isso permita que o aplicativo controle sua "aparência", ele pode forçar o aplicativo a conter código específico do driver. Isso ocorre quando o aplicativo precisa solicitar ao usuário informações de conexão específicas do driver. Isso apresenta uma situação impossível para aplicativos genéricos, que são projetados para trabalhar com todo e qualquer driver, incluindo drivers que não existem quando o aplicativo é escrito.  
  
 **O SQLDriverConnect** pode solicitar informações ao usuário sobre a conexão. Por exemplo, o programa personalizado mencionado anteriormente poderia passar a seguinte seqüência de conexão para **SQLDriverConnect**:  
  
```  
DSN=XYZ Corp;  
```  
  
 O driver pode então exibir uma caixa de diálogo que solicita IDs e senhas de usuário, semelhante à ilustração a seguir.  
  
 ![Caixa de diálogo que solicita IDs e senhas do usuário](../../../odbc/reference/develop-app/media/pr18.gif "pr18")  
  
 Que o driver pode solicitar informações de conexão é particularmente útil para aplicativos genéricos e verticais. Esses aplicativos não devem conter informações específicas do motorista, e ter o prompt do motorista para as informações que precisa mantém essas informações fora do aplicativo. Isso é mostrado pelos dois exemplos anteriores. Quando o aplicativo passou apenas o nome de origem dos dados para o motorista, o aplicativo não continha nenhuma informação específica do motorista e, portanto, não estava vinculado a um driver específico. Quando o aplicativo passou uma seqüência de conexão completa para o driver, ele estava ligado ao driver que podia interpretar essa string.  
  
 Um aplicativo genérico pode levar isso um passo adiante e nem mesmo especificar uma fonte de dados. Quando **o SQLDriverConnect** recebe uma seqüência de conexão vazia, o Gerenciador de driver exibe a seguinte caixa de diálogo.  
  
 ![Caixa de diálogo Selecionar Fonte de Dados](../../../odbc/reference/develop-app/media/ch06a.gif "CH06A")  
  
 Depois que o usuário seleciona uma fonte de dados, o Gerenciador de driver constrói uma seqüência de conexão especificando essa fonte de dados e passa-a para o driver. O driver pode, então, solicitar ao usuário qualquer informação adicional que precise.  
  
 As condições sob as quais o driver solicita ao usuário são controladas pelo sinalizador *DriverComplet;* há opções para sempre solicitar, solicitar, se necessário, ou nunca solicitar. Para obter uma descrição completa deste sinalizador, consulte a descrição da função [SQLDriverConnect.](../../../odbc/reference/syntax/sqldriverconnect-function.md)
