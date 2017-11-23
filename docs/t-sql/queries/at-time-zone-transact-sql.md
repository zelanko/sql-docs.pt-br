---
title: "NO FUSO horário (Transact-SQL) | Microsoft Docs"
ms.date: 11/16/2016
ms.prod: sql-non-specified
ms.prod_service: database-engine, sql-database
ms.service: 
ms.component: t-sql|queries
ms.reviewer: 
ms.suite: sql
ms.custom: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords: AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
caps.latest.revision: "13"
author: BYHAM
ms.author: rickbyh
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: 2265efe9fab240d25d03e3e1ef16009d294166af
ms.sourcegitcommit: 66bef6981f613b454db465e190b489031c4fb8d3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="at-time-zone-transact-sql"></a>NO FUSO horário (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  Converte um *inputdate* para correspondente *datetimeoffset* valor no fuso horário de destino. Se *inputdate* é fornecido sem informação de deslocamento, a função aplicará o deslocamento do fuso horário, supondo que *inputdate* valor é fornecido no fuso horário de destino. Se *inputdate* é fornecido como um *datetimeoffset* valor, que **AT TIME ZONE** cláusula converte-o para o fuso horário de destino usando regras de conversão de fuso horário.  
  
 **NO FUSO horário** implementação depende de um mecanismo do Windows para converter **datetime** valores entre fusos horários.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Topic link icon") [Convenções da sintaxe Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>Argumentos  
 *inputdate*  
 É uma expressão que pode ser resolvida para um **smalldatetime**, **datetime**, **datetime2**, ou **datetimeoffset** valor.  
  
 *fuso horário*  
 Nome da zona de tempo de destino. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]se baseia em fusos horários que são armazenados no registro do Windows. Todos os fusos horários instalados no computador são armazenados no hive do registro a seguir: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**. Uma lista de fusos horários instalados também é exposta por meio de [time_zone_info &#40; Transact-SQL &#41; ](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md) exibição.  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados **datetimeoffset**  
  
## <a name="return-value"></a>Valor de retorno  
 O **datetimeoffset** valor no fuso horário de destino.  
  
## <a name="remarks"></a>Comentários  
 **NO FUSO horário** aplica regras específicas para converter valores de entrada na **smalldatetime**, **datetime** e **datetime2** tipos de dados, que se encaixam em uma intervalo é afetado pela alteração DST:  
  
-   Quando o relógio está definido em frente e há uma lacuna na hora local, duração da qual depende a duração do ajuste de relógio (geralmente 1 hora, mas ele pode ser 30 ou 45 minutos, dependendo de fuso horário). Nesse caso, os pontos no tempo que pertencem a essa lacuna são convertidos com deslocamento *depois* alteração do horário de verão.  
  
    ```  
    /*  
        Moving to DST in "Central European Standard Time" zone: 
        offset changes from +01:00 -> +02:00   
        Change occurred on March 29th, 2015 at 02:00:00.   
        Adjusted local time became 2015-03-29 03:00:00.  
    */  
    
    --Time before DST change has standard time offset (+01:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T01:01:00', 126)     
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 01:01:00 +01:00   
  
    /*
      Adjusted time from the "gap interval" (between 02:00 and 03:00)
      is moved 1 hour ahead and presented with the summer time offset
      (after the DST change) 
    */
    SELECT CONVERT(datetime2(0), '2015-03-29T02:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00
      
    --Time after 03:00 is presented with the summer time offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-03-29T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-03-29 03:01:00 +02:00  
  
    ```  
  
- Quando o relógio for alterado, 2 horas da hora local são sobrepostas em uma hora.  Nesse caso, os pontos no tempo que pertencem ao intervalo sobreposto são apresentados com o deslocamento *antes de* a alteração do relógio:  
  
    ```  
    /*  
        Moving back from DST to standard time in 
        "Central European Standard Time" zone: 
        offset changes from +02:00 -> +01:00.  
        Change occurred on October 25th, 2015 at 03:00:00.   
        Adjusted local time became 2015-10-25 02:00:00   
    */  
    
    --Time before the change has DST offset (+02:00)
    SELECT CONVERT(datetime2(0), '2015-10-25T01:01:00', 126)      
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 01:01:00 +02:00  
    
    /*
      Time from the "overlapped interval" is presented with standard time 
      offset (before the change)    
    */
    SELECT CONVERT(datetime2(0), '2015-10-25T02:00:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 02:00:00 +02:00  
    
    
    --Time after 03:00 is regularly presented with the standard time offset (+01:00)    
    SELECT CONVERT(datetime2(0), '2015-10-25T03:01:00', 126)   
    AT TIME ZONE 'Central European Standard Time';  
    --Result: 2015-10-25 03:01:00 +01:00
  
    ```  

Já que algumas informações (como as regras de fuso horário) são mantidas fora do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e estão sujeitos a alterações ocasionais, o **AT TIME ZONE** função é classificada como não determinísticas. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. Adicionar um deslocamento de fuso horário de destino para datetime sem informação de deslocamento  
 Use **AT TIME ZONE** para adicionar um deslocamento com base nas regras de fuso horário quando você sabe que o original **datetime** valores são fornecidos no mesmo fuso horário:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="b-convert-values-between-different-time-zones"></a>B. Converter valores entre fusos horários diferentes  
 O exemplo a seguir converte os valores entre fusos horários diferentes:  
  
```  
USE AdventureWorks2016;  
GO  
  
SELECT SalesOrderID, OrderDate,   
    OrderDate AT TIME ZONE 'Pacific Standard Time' AS OrderDate_TimeZonePST,  
    OrderDate AT TIME ZONE 'Pacific Standard Time'   
    AT TIME ZONE 'Central European Standard Time' AS OrderDate_TimeZoneCET  
FROM Sales.SalesOrderHeader;  
```  
  
### <a name="c-query-temporal-tables-using-local-time-zone"></a>C. Consultar tabelas temporais usando o fuso horário local  
 O exemplo a seguir seleciona os dados de uma tabela temporal.  
  
```  
USE AdventureWorks2016;  
GO  
  
DECLARE @ASOF datetimeoffset;  
SET @ASOF = DATEADD (month, -1, GETDATE()) AT TIME ZONE 'UTC';  
  
-- Query state of the table a month ago projecting period   
-- columns as Pacific Standard Time  
SELECT BusinessEntityID, PersonType, NameStyle, Title,   
    FirstName, MiddleName,  
    ValidFrom AT TIME ZONE 'Pacific Standard Time' 
FROM  Person.Person_Temporal  
FOR SYSTEM_TIME AS OF @ASOF;  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tipos de data e hora](../../t-sql/data-types/date-and-time-types.md)   
 [Dados de data e hora tipos e funções &#40; Transact-SQL &#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
  
