---
title: sp_sequence_get_range (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-data-warehouse
ms.reviewer: ''
ms.technology: system-objects
ms.topic: language-reference
f1_keywords:
- sp_sequence_get_range
- sp_sequence_get_range_TSQL
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, sp_sequence_get_range procedure
- sp_sequence_get_range
ms.assetid: 8ca6b0c6-8d9c-4eee-b02f-51ddffab4492
author: stevestein
ms.author: sstein
monikerRange: =azuresqldb-current||=azure-sqldw-latest||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: 9e92b9ec98ee08579164c403fe1be6ff6ef47816
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "68104502"
---
# <a name="spsequencegetrange-transact-sql"></a>sp_sequence_get_range (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-asdw-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-asdw-xxx-md.md)]

  Retorna um intervalo de valores de sequência de um objeto de sequência. O objeto de sequência gera e emite o número de valores solicitado e fornece o aplicativo com metadados relacionados ao intervalo.  
  
 Para obter mais informações sobre números de sequência, consulte [números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
sp_sequence_get_range [ @sequence_name = ] N'<sequence>'   
     , [ @range_size = ] range_size  
     , [ @range_first_value = ] range_first_value OUTPUT   
    [, [ @range_last_value = ] range_last_value OUTPUT ]  
    [, [ @range_cycle_count = ] range_cycle_count OUTPUT ]  
    [, [ @sequence_increment = ] sequence_increment OUTPUT ]  
    [, [ @sequence_min_value = ] sequence_min_value OUTPUT ]  
    [, [ @sequence_max_value = ] sequence_max_value OUTPUT ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
`[ @sequence_name = ] N'sequence'` O nome do objeto de sequência. O esquema é opcional. *sequence_name* está **nvarchar(776)** .  
  
`[ @range_size = ] range_size` O número de valores a ser buscado da sequência. **@range_size** está **bigint**.  
  
`[ @range_first_value = ] range_first_value` Parâmetro de saída retorna o primeiro valor (mínimo ou máximo) o objeto de sequência usado para calcular o intervalo solicitado. **@range_first_value** está **sql_variant** com o mesmo tipo base que o objeto de sequência usado na solicitação.  
  
`[ @range_last_value = ] range_last_value` Parâmetro de saída opcional retorna o último valor do intervalo solicitado. **@range_last_value** está **sql_variant** com o mesmo tipo base que o objeto de sequência usado na solicitação.  
  
`[ @range_cycle_count = ] range_cycle_count` Parâmetro de saída opcional retorna o número de vezes que o objeto de sequência alternado para retornar o intervalo solicitado. **@range_cycle_count** está **int**.  
  
`[ @sequence_increment = ] sequence_increment` Parâmetro de saída opcional retorna o incremento do objeto de sequência usado para calcular o intervalo solicitado. **@sequence_increment** está **sql_variant** com o mesmo tipo base que o objeto de sequência usado na solicitação.  
  
`[ @sequence_min_value = ] sequence_min_value` Parâmetro de saída opcional retorna o valor mínimo do objeto de sequência. **@sequence_min_value** está **sql_variant** com o mesmo tipo base que o objeto de sequência usado na solicitação.  
  
`[ @sequence_max_value = ] sequence_max_value` Parâmetro de saída opcional retorna o valor máximo do objeto de sequência. **@sequence_max_value** está **sql_variant** com o mesmo tipo base que o objeto de sequência usado na solicitação.  
  
## <a name="return-code-values"></a>Valores do código de retorno  
 0 (êxito) ou 1 (falha)  
  
## <a name="remarks"></a>Comentários  
 sp_sequence_get_rangeis no sys. esquema e pode ser referenciado como sys.sp_sequence_get_range.  
  
### <a name="cycling-sequences"></a>Sequências de ciclo  
 Se preciso for, o objeto de sequência vai realizar um ciclo do número apropriado de vezes para atender ao intervalo solicitado. O número de vezes em que o ciclo é retornado para o chamador pelo parâmetro `@range_cycle_count`.  
  
> [!NOTE]  
>  Ao realizar o ciclo, um objeto de sequência reinicia a partir do valor mínimo para uma sequência ascendente e do valor máximo para uma sequência decrescente, não a partir do valor inicial do objeto de sequência.  
  
### <a name="non-cycling-sequences"></a>Sequências não cíclicas  
 Se o número de valores no intervalo solicitado for maior que os valores disponíveis restantes no objeto de sequência, o intervalo solicitado não será deduzido do objeto de sequência e o erro 11732 a seguir será retornado:  
  
 `The requested range for sequence object '%.*ls' exceeds the maximum or minimum limit. Retry with a smaller range.`  
  
## <a name="permissions"></a>Permissões  
 Requer permissão UPDATE no objeto de sequência ou o esquema do objeto de sequência.  
  
## <a name="examples"></a>Exemplos  
 Os exemplos seguintes usam um objeto de sequência chamado Test.RangeSeq. Use a seguinte instrução para criar a sequência de Test.RangeSeq.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.RangeSeq  
    AS int   
    START WITH 1  
    INCREMENT BY 1  
    MINVALUE 1  
    MAXVALUE 25  
    CYCLE  
    CACHE 10  
;  
```  
  
### <a name="a-retrieving-a-range-of-sequence-values"></a>A. Recuperando um intervalo de valores de sequência  
 A instrução a seguir obtém quatro números de sequência do objeto de sequência Test.RangeSeq e retorna o primeiro número ao usuário.  
  
```  
DECLARE @range_first_value sql_variant ,   
        @range_first_value_output sql_variant ;  
  
EXEC sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 4  
, @range_first_value = @range_first_value_output OUTPUT ;  
  
SELECT @range_first_value_output AS FirstNumber ;  
  
```  
  
### <a name="b-returning-all-output-parameters"></a>B. Retornando todos os parâmetros de saída  
 O exemplo a seguir retorna todos os valores de saída do procedimento sp_sequence_get_range.  
  
```  
DECLARE    
  @FirstSeqNum sql_variant  
, @LastSeqNum sql_variant  
, @CycleCount int  
, @SeqIncr sql_variant  
, @SeqMinVal sql_variant  
, @SeqMaxVal sql_variant ;  
  
EXEC sys.sp_sequence_get_range  
@sequence_name = N'Test.RangeSeq'  
, @range_size = 5  
, @range_first_value = @FirstSeqNum OUTPUT   
, @range_last_value = @LastSeqNum OUTPUT   
, @range_cycle_count = @CycleCount OUTPUT  
, @sequence_increment = @SeqIncr OUTPUT  
, @sequence_min_value = @SeqMinVal OUTPUT  
, @sequence_max_value = @SeqMaxVal OUTPUT ;  
  
-- The following statement returns the output values  
SELECT  
  @FirstSeqNum AS FirstVal  
, @LastSeqNum AS LastVal  
, @CycleCount AS CycleCount  
, @SeqIncr AS SeqIncrement  
, @SeqMinVal AS MinSeq  
, @SeqMaxVal AS MaxSeq ;  
  
```  
  
 Alterar o argumento `@range_size` para um número grande como 75 fará o objeto de sequência realizar um ciclo. Verifique o argumento `@range_cycle_count` para determinar se e quantas vezes o objeto de sequência realizou o ciclo.  
  
### <a name="c-example-using-adonet"></a>C. Exemplo: usando ADO.NET  
 O exemplo a seguir obtém um intervalo da Test.RangeSeq usando o ADO.NET.  
  
```  
SqlCommand cmd = new SqlCommand();  
cmd.Connection = conn;  
cmd.CommandType = CommandType.StoredProcedure;  
cmd.CommandText = "sys.sp_sequence_get_range";  
cmd.Parameters.AddWithValue("@sequence_name", "Test.RangeSeq");  
cmd.Parameters.AddWithValue("@range_size", 10);  
  
// Specify an output parameter to retreive the first value of the generated range.  
SqlParameter firstValueInRange = new SqlParameter("@range_first_value", SqlDbType.Variant);  
firstValueInRange.Direction = ParameterDirection.Output;  
cmd.Parameters.Add(firstValueInRange);  
  
conn.Open();  
cmd.ExecuteNonQuery();  
  
// Output the first value of the generated range.  
Console.WriteLine(firstValueInRange.Value);  
  
```  
  
## <a name="see-also"></a>Consulte também  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [ALTER SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md)  
  
  
