---
title: Mensagens de erro
description: As mensagens de erro do PDW (data warehouse paralelo) relatam erros e problemas encontrados pelos componentes do PDW e também podem incluir SQL Server erros na superfície do PDW. Essas mensagens de erro usam uma sintaxe consistente para apresentar informações. Entender essa sintaxe permitirá que você identifique e corrija os problemas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 2d89e80a89df53e85ef8d2bf53c369d9e4dc0d49
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "74401161"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Mensagens de erro em paralelo data warehouse

As mensagens de erro do PDW (data warehouse paralelo) relatam erros e problemas encontrados pelos componentes do PDW e também podem incluir SQL Server erros na superfície do PDW. Essas mensagens de erro usam uma sintaxe consistente para apresentar informações. Entender essa sintaxe permitirá que você identifique e corrija problemas em SQL Server PDW.  
  
## <a name="error-message-basics"></a><a name="Basics"></a>Noções básicas de mensagem de erro  
As mensagens de erro retornadas seguem a mesma sintaxe.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estes são os valores possíveis para cada campo:  
  
|Campo|Descrição|Exemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|A palavra "erro" ou outro texto alertando o usuário sobre um problema.|ERROR|  
|*SQL_State_Code*|O código do estado SQL, de acordo com a especificação ODBC. O driver gera o código de estado SQL apropriado sempre que retorna uma mensagem para um aplicativo. O texto "Microsoft" indica a origem do erro.|42000|  
|*Driver_Details*|Detalhes dependentes do driver, como o tipo de driver usado.|Driver de data warehouse paralelo do ODBC SQL Server 2008 R2|  
|*QueryID*|O identificador exclusivo da consulta. Use esse valor para encontrar informações adicionais relacionadas ao processamento da consulta. Por exemplo, os detalhes de execução da consulta podem ser encontrados no console de administração usando a ID de consulta. Para obter mais informações, consulte [monitorar o dispositivo usando o console de administração](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Se uma QueryId não for aplicável, o texto "Internal" será retornado ao usuário.|QID2377|  
|*Message_String*|Uma descrição legível do erro ou do problema. Ao retornar SQL Server erros, esse é o texto da mensagem SQL Server.|Somente a atribuição igual pode aparecer na lista de conjuntos de uma instrução UPDATE.|  
  
Esses valores de exemplo seriam apresentados ao usuário como este:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Consulte Também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Noções básicas sobre alertas do console de admin](understanding-admin-console-alerts.md)  
  
