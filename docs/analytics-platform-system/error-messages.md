---
title: Mensagens de erro (SQL Server PDW)
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: analytics-platform-system
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: 
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: e6223cba-2dec-4b8a-bc10-e2ef6a821fe0
caps.latest.revision: "9"
ms.openlocfilehash: c9c0ebf9b452fdf2ec54ae84bec34288e73e88aa
ms.sourcegitcommit: cc71f1027884462c359effb898390c8d97eaa414
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="error-messages"></a>Mensagens de erro
Mensagens de erro do SQL Server PDW relatam erros e problemas encontrados pelos componentes do SQL Server PDW e também podem incluir erros do SQL Server expostos por meio do SQL Server PDW. Essas mensagens de erro usam uma sintaxe consistente de apresentação de informações. Noções básicas sobre essa sintaxe permitirá que você identifique e corrija os problemas no SQL Server PDW.  
  
## <a name="Basics"></a>Noções básicas de mensagem de erro  
Mensagens de erro retornadas seguem a mesma sintaxe.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estes são os valores possíveis para cada campo:  
  
|Campo|Description|Exemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|A palavra "ERROR" ou outro texto a alertar o usuário a um problema.|erro|  
|*SQL_State_Code*|O código de estado SQL, de acordo com a especificação de ODBC. O driver gera o código de estado SQL apropriado sempre retornará uma mensagem para um aplicativo. O texto "Microsoft" indica a origem do erro.|42000|  
|*Driver_Details*|Detalhes do driver dependente, como o tipo de driver usado.|Driver ODBC SQL Server 2008 R2 Parallel Data Warehouse|  
|*QueryID*|O identificador exclusivo para a consulta. Use esse valor para localizar informações adicionais relacionadas ao processamento de consulta. Por exemplo, os detalhes de execução de consulta podem ser encontrados no Console do administrador usando a ID de consulta. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Se um QueryID não for aplicável, o texto "Interno" é retornado para o usuário.|QID2377|  
|*Message_String*|Uma descrição legível do erro ou problema. Ao retornar erros do SQL Server, isso é o texto da mensagem do SQL Server.|Apenas a atribuição igual pode aparecer na lista de conjuntos de uma instrução UPDATE.|  
  
Esses valores de exemplo deve ser apresentadas ao usuário como este:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Compreendendo os alertas do Console de administração](understanding-admin-console-alerts.md)  
  
