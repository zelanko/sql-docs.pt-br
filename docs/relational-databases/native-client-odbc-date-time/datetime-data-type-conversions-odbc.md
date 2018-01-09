---
title: "DateTime conversões de tipo de dados (ODBC) | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database, sql-data-warehouse, pdw
ms.service: 
ms.component: native-client-odbc-date-time
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- conversions [ODBC]
- bindings [ODBC]
- ODBC, bindings and conversions
ms.assetid: 66b9d282-c88d-40e5-93c2-fd5499a74458
caps.latest.revision: "19"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 065c030e38e588dbc1068ead291f0ac4f5a6a179
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="datetime-data-type-conversions-odbc"></a>Conversões do tipo de dados datetime (ODBC)
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)]
[!INCLUDE[SNAC_Deprecated](../../includes/snac-deprecated.md)]

  As conversões a seguir já estão definidas pelo ODBC ou são uma extensão consistente do ODBC. As conversões fornecidas por cada provedor são determinadas pela comunidade atendida pelo provedor e, com frequência, existem inconsistências entre os resultados. Os valores entre colchetes são opcionais.  
  
-   O formato de cadeias de caracteres datetime é 'aaaa-mm-dd[ hh:mm:ss[.9999999][ mais/menos hh:mm]]'  
  
-   O formato de cadeias de caracteres de hora é 'hh:mm:ss[.9999999]'  
  
-   O formato de cadeias de caracteres de data é 'aaaa-mm-dd'  
  
 As conversões de cadeias de caracteres permitem uma flexibilidade nos espaços em branco e na largura dos campos. Para obter mais informações, consulte a seção "Formatos de dados: cadeias e literais" [suporte de tipo de dados para aprimoramentos de hora e data de ODBC](../../relational-databases/native-client-odbc-date-time/data-type-support-for-odbc-date-and-time-improvements.md).  
  
 Seguem as regras de conversão gerais:  
  
-   Se não houver uma hora mas o receptor puder armazenar horas, a hora será definida como zero.  
  
-   Se não houver uma data presente, mas o receptor puder armazenar datas, a data atual será usada.  
  
-   Se não houver um fuso horário presente no tipo de dados que o cliente está utilizando, mas o servidor puder armazenar fusos horários, a data será armazenada no fuso horário do cliente. Observe que isso é diferente do comportamento do servidor.  
  
-   Se não houver um fuso horário presente no tipo do servidor, mas o tipo do cliente tiver um fuso horário, a hora será convertida para UTC antes de ser armazenada no servidor.  
  
-   Se houver uma hora presente, mas o receptor não puder armazenar horas, o componente de hora será ignorado.  
  
-   Se houver uma data presente, mas o receptor não puder armazenar datas, o componente de data será ignorado.  
  
-   Se ocorrer o truncamento de segundos ou frações de segundos ao converter do C para o SQL, um registro de diagnóstico será gerado com SQLSTATE 22008 e a mensagem "Estouro do campo datetime".  
  
-   Se ocorrer o truncamento de segundos ou frações de segundos ao converter do SQL para o C, um registro de diagnóstico será gerado com SQLSTATE 01S07 e a mensagem "Truncamento de frações".  
  
## <a name="in-this-section"></a>Nesta seção  
 [Conversões de C para SQL](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-c-to-sql.md)  
 Lista os problemas a serem considerados ao converter tipos do C em tipos de data/hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 [Conversões de SQL para C](../../relational-databases/native-client-odbc-date-time/datetime-data-type-conversions-from-sql-to-c.md)  
 Lista os problemas a serem considerados ao converter tipos de data/hora do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em tipos do C.  
  
## <a name="see-also"></a>Consulte Também  
 [Data e hora melhorias &#40; ODBC &#41;](../../relational-databases/native-client-odbc-date-time/date-and-time-improvements-odbc.md)  
  
  
