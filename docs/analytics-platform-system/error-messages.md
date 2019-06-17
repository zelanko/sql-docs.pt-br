---
title: Mensagens de erro – Parallel Data Warehouse | Microsoft Docs
description: Mensagens de erro do Parallel Data Warehouse (PDW) relatam erros e problemas encontrados pelos componentes do PDW e também podem incluir erros do SQL Server exibidos por meio do PDW. Essas mensagens de erro usam uma sintaxe consistente para apresentar informações. Noções básicas sobre essa sintaxe permitirá que você identifique e corrija os problemas.
author: mzaman1
manager: craigg
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.openlocfilehash: 3ffc7a097845f4652f56d82c572ecfab868d33f1
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63042590"
---
# <a name="error-messages-in-parallel-data-warehouse"></a>Mensagens de erro no Parallel Data Warehouse

Mensagens de erro do Parallel Data Warehouse (PDW) relatam erros e problemas encontrados pelos componentes do PDW e também podem incluir erros do SQL Server exibidos por meio do PDW. Essas mensagens de erro usam uma sintaxe consistente para apresentar informações. Noções básicas sobre essa sintaxe permitirá que você identifique e corrija os problemas no SQL Server PDW.  
  
## <a name="Basics"></a>Noções básicas sobre mensagem de erro  
Mensagens de erro que são retornadas seguem a mesma sintaxe.  
  
`Error_Indicator [SQL_State_Code] [Driver_Details] [QueryID] Message_String`  
  
Estes são os valores possíveis para cada campo:  
  
|Campo|Descrição|Exemplo|  
|---------|---------------|-----------|  
|*Error_Indicator*|A palavra "ERROR" ou outro texto alertando o usuário a um problema.|erro|  
|*SQL_State_Code*|O código de estado SQL, de acordo com a especificação de ODBC. O driver vai gerar o código de estado SQL apropriado sempre que ele retorna uma mensagem para um aplicativo. O texto "Microsoft" indica a origem do erro.|42000|  
|*Driver_Details*|Detalhes de dependente do driver, como o tipo de driver usado.|Driver ODBC SQL Server 2008 R2 Parallel Data Warehouse|  
|*QueryID*|O identificador exclusivo para a consulta. Use esse valor para localizar informações adicionais relacionadas ao processamento da consulta. Por exemplo, os detalhes da execução de consulta podem ser encontrados no Console do administrador usando a ID da consulta. Para obter mais informações, consulte [monitorar o dispositivo usando o Console de administração](monitor-the-appliance-by-using-the-admin-console.md).<br /><br />Se um QueryID não for aplicável, o texto "Interno" é retornado para o usuário.|QID2377|  
|*Message_String*|Uma descrição legível do erro ou problema. Quando o retorno de erros do SQL Server, esse é o texto da mensagem do SQL Server.|Somente a atribuição igual pode aparecer na lista de conjuntos de uma instrução UPDATE.|  
  
Esses valores de exemplo serão apresentadas ao usuário como este:  
  
`ERROR [42000] [Microsoft][ODBC SQL Server 2008 R2 Parallel Data Warehouse driver][QID2380]Only equal assignment can appear in the set list of an UPDATE statement.`  
  
## <a name="see-also"></a>Consulte também  
<!-- MISSING LINKS 
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
[Noções básicas sobre alertas do Console de administração](understanding-admin-console-alerts.md)  
  
