---
title: AT TIME ZONE (Transact-SQL) | Microsoft Docs
ms.date: 11/16/2016
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.custom: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- AT TIME ZONE
- AT_TIME_ZONE_TSQL
helpviewer_keywords:
- AT TIME ZONE function
ms.assetid: 311f682f-7f1b-43b6-9ea0-24e36b64f73a
author: VanMSFT
ms.author: vanto
manager: craigg
monikerRange: = azuresqldb-current ||>= sql-server-2016 ||>= sql-server-linux-2017 ||= azure-sqldw-latest ||= sqlallproducts-allversions
ms.openlocfilehash: c3601e341205cc41a2da3991b4de434166f246a1
ms.sourcegitcommit: ccea98fa0768d01076cb6ffef0b4bdb221b2f9d5
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/13/2019
ms.locfileid: "65560189"
---
# <a name="at-time-zone-transact-sql"></a>AT TIME ZONE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2016-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2016-asdb-asdw-xxx-md.md)]

  Converte um *inputdate* para o valor de *datetimeoffset* correspondente no fuso horário de destino. Quando *inputdate* é fornecido sem as informação de diferença, a função aplica a diferença do fuso horário considerando que *inputdate* está no fuso horário de destino. Se *inputdate* for fornecido como um valor de *datetimeoffset*, a cláusula **AT TIME ZONE** o converterá no fuso horário de destino usando regras de conversão de fuso horário.  
  
 A implementação de **AT TIME ZONE** depende de um mecanismo do Windows para converter os valores de **datetime** entre fusos horários.  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
inputdate AT TIME ZONE timezone  
```  
  
## <a name="arguments"></a>Argumentos  
 *inputdate*  
 É uma expressão que pode ser resolvida para um valor de **smalldatetime**, **datetime**, **datetime2** ou **datetimeoffset**.  
  
 *timezone*  
 Nome do fuso horário de destino. O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] baseia-se nos fusos horários armazenados no Registro do Windows. Os fusos horários instalados no computador são armazenados no hive do Registro a seguir: **KEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Windows NT\CurrentVersion\Time Zones**. Uma lista dos fusos horários instalados também é exposta por meio da exibição [sys.time_zone_info &#40;Transact-SQL&#41;](../../relational-databases/system-catalog-views/sys-time-zone-info-transact-sql.md).  
  
## <a name="return-types"></a>Tipos de retorno  
 Retorna o tipo de dados de **datetimeoffset**.  
  
## <a name="return-value"></a>Valor retornado  
 O valor de **datetimeoffset** no fuso horário de destino.  
  
## <a name="remarks"></a>Remarks  
 **AT TIME ZONE** aplica regras específicas para converter os valores de entrada nos tipos de dados **smalldatetime**, **datetime** e **datetime2**, que caem em um intervalo afetado por uma alteração de horário de verão:  
  
-   Quando o relógio está adiantado, há uma lacuna na hora local igual à duração do ajuste do relógio. Esta duração é geralmente de 1 hora, mas pode ser de 30 ou 45 minutos, dependendo do fuso horário. Os pontos no tempo que pertencem a essa diferença são convertidos com a diferença *depois* da alteração do horário de verão.  
  
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
  
- Quando o relógio for alterado novamente, 2 horas da hora local serão sobrepostas em uma hora.  Nesse caso, os pontos no tempo que pertencem ao intervalo sobreposto são apresentados com a diferença *antes* da alteração do relógio:  
  
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

Como algumas informações (como as regras de fuso horário) são mantidas fora do [!INCLUDE[ssNoVersion_md](../../includes/ssnoversion-md.md)] e estão sujeitas a alterações ocasionais, a função **AT TIME ZONE** é classificada como não determinísticas. 
  
## <a name="examples"></a>Exemplos  
  
### <a name="a-add-target-time-zone-offset-to-datetime-without-offset-information"></a>A. Adicionar uma diferença de fuso horário de destino para datetime sem informação de diferença  
 Use **AT TIME ZONE** para adicionar uma diferença com base nas regras de fuso horário quando você souber que os valores de **datetime** originais são fornecidos no mesmo fuso horário:  
  
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
  
## <a name="see-also"></a>Consulte Também  
 [Tipos de data e hora](../../t-sql/data-types/date-and-time-types.md)   
 [Tipos de dados e funções de data e hora &#40;Transact-SQL&#41;](../../t-sql/functions/date-and-time-data-types-and-functions-transact-sql.md)  
  
