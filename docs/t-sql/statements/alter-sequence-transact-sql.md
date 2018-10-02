---
title: ALTER SEQUENCE (Transact-SQL) | Microsoft Docs
ms.custom: ''
ms.date: 08/08/2015
ms.prod: sql
ms.prod_service: database-engine, sql-database
ms.reviewer: ''
ms.technology: t-sql
ms.topic: language-reference
f1_keywords:
- ALTER_SEQUENCE_TSQL
- ALTER SEQUENCE
dev_langs:
- TSQL
helpviewer_keywords:
- sequence number object, altering
- ALTER SEQUENCE statement
ms.assetid: decc0760-029e-4baf-96c9-4a64073df1c2
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f0b85a5127a71b19e090ccc9bff1f018cc803b1d
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47685376"
---
# <a name="alter-sequence-transact-sql"></a>ALTER SEQUENCE (Transact-SQL)
[!INCLUDE[tsql-appliesto-ss2012-asdb-xxxx-xxx-md](../../includes/tsql-appliesto-ss2012-asdb-xxxx-xxx-md.md)]

  Modifica os argumentos de um objeto de sequência existente. Se a sequência tiver sido criada com a opção **CACHE**, alterar a sequência recriará o cache.  
  
 Os objetos de sequência são criados usando a instrução [CREATE SEQUENCE](../../t-sql/statements/create-sequence-transact-sql.md). As sequências são valores inteiros e podem ser de qualquer tipo de dados que retorne um inteiro. O tipo de dados não pode ser alterado com a instrução ALTER SEQUENCE. Para alterar o tipo de dados, remova e crie o objeto de sequência.  
  
 Uma sequência é um objeto associado a um esquema definido pelo usuário que gera uma sequência de valores numéricos de acordo com uma especificação. Novos valores são gerados a partir de uma sequência ao chamar a função NEXT VALUE FOR. Use **sp_sequence_get_range** para obter vários números de sequência de uma vez. Para obter informações e cenários que usam CREATE SEQUENCE, **sp_sequence_get_range** e a função NEXT VALUE FOR, veja [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
 ![Ícone de link do tópico](../../database-engine/configure-windows/media/topic-link.gif "Ícone de link do tópico") [Convenções de sintaxe de Transact-SQL](../../t-sql/language-elements/transact-sql-syntax-conventions-transact-sql.md)  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
ALTER SEQUENCE [schema_name. ] sequence_name  
    [ RESTART [ WITH <constant> ] ]  
    [ INCREMENT BY <constant> ]  
    [ { MINVALUE <constant> } | { NO MINVALUE } ]  
    [ { MAXVALUE <constant> } | { NO MAXVALUE } ]  
    [ CYCLE | { NO CYCLE } ]  
    [ { CACHE [ <constant> ] } | { NO CACHE } ]  
    [ ; ]  
```  
  
## <a name="arguments"></a>Argumentos  
 *sequence_name*  
 Especifica o nome exclusivo pelo qual a sequência é conhecida no banco de dados. O tipo é **sysname**.  
  
 RESTART [ WITH \<constant> ]  
 O próximo valor que será retornado pelo objeto de sequência. Se fornecido, o valor de RESTART WITH deverá ser um inteiro menor ou igual ao valor máximo e maior ou igual ao valor mínimo do objeto de sequência. Se o valor de WITH for omitido, a numeração da sequência reiniciará com base nas opções CREATE SEQUENCE originais.  
  
 INCREMENT BY \<constant>  
 O valor usado para incrementar (ou diminuir, se negativo) o valor base do objeto de sequência de cada chamada para a função NEXT VALUE FOR. Se o incremento for um valor negativo, o objeto de sequência será decrescente; caso contrário, será crescente. O incremento não pode ser 0.  
  
 [ MINVALUE \<constant> | NO MINVALUE ]  
 Especifica os limites do objeto de sequência. Se NO MINVALUE for especificado, o valor mínimo possível do tipo de dados de sequência será usado.  
  
 [ MAXVALUE \<constant> | NO MAXVALUE  
 Especifica os limites do objeto de sequência. Se NO MAXVALUE for especificado, o valor máximo possível do tipo de dados de sequência será usado.  
  
 [ CYCLE | NO CYCLE ]  
 Essa propriedade especifica se o objeto de sequência deve reiniciar a partir do valor mínimo (ou máximo para objetos de sequência decrescentes) ou gerar uma exceção quando seu valor mínimo ou máximo for excedido.  
  
> [!NOTE]  
>  Após o ciclo, o próximo valor é o valor mínimo ou máximo, e não o START VALUE da sequência.  
  
 [ CACHE [\<constant> ] | NO CACHE ]  
 Aumenta o desempenho de aplicativos que usam objetos de sequência por meio da minimização do número de E/S necessárias para persistir os valores gerados para as tabelas do sistema.  
  
 Para obter mais informações sobre o comportamento do cache, veja [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
## <a name="remarks"></a>Remarks  
 Para obter informações sobre como as sequências são criadas e como o cache de sequências é gerenciado, veja [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md).  
  
 O MINVALUE de sequências crescentes e o MAXVALUE de sequências decrescentes não podem ser alterados para um valor que não permita o valor START VALUE da sequência. Para alterar o MINVALUE de uma sequência crescente para um número maior que o valor de START WITH ou para alterar o MAXVALUE de uma sequência decrescente para um número menor que o valor de START WITH, inclua o argumento RESTART WITH para reiniciar a sequência em um ponto desejado que esteja dentro do intervalo mínimo e máximo.  
  
## <a name="metadata"></a>Metadados  
 Para obter informações sobre sequências, consulte [sys.sequences](../../relational-databases/system-catalog-views/sys-sequences-transact-sql.md).  
  
## <a name="security"></a>Segurança  
  
### <a name="permissions"></a>Permissões  
 Exige a permissão **ALTER** na sequência ou a permissão **ALTER** no esquema. Para conceder a permissão **ALTER** na sequência, use **ALTER ON OBJECT** no seguinte formato:  
  
```  
GRANT ALTER ON OBJECT::Test.TinySeq TO [AdventureWorks\Larry]  
```  
  
 A propriedade de um objeto de sequência pode ser transferida com o uso da instrução **ALTER AUTHORIZATION**.  
  
### <a name="audit"></a>Auditar o  
 Para auditar **ALTER SEQUENCE**, monitore o **SCHEMA_OBJECT_CHANGE_GROUP**.  
  
## <a name="examples"></a>Exemplos  
 Para obter exemplos de como criar sequências e usar a função **NEXT VALUE FOR** para gerar números de sequência, consulte [Números de sequência](../../relational-databases/sequence-numbers/sequence-numbers.md).  
  
### <a name="a-altering-a-sequence"></a>A. Alterando uma sequência  
 O exemplo a seguir cria um esquema chamado Test e uma sequência chamada TestSeq usando o tipo de dados **int** com um intervalo de 0 a 255. A sequência começa com 125 e é incrementada em 25 sempre que um número é gerado. Como a sequência é configurada para executar um ciclo, quando o valor excede o valor máximo de 200, a sequência é reiniciada no valor mínimo de 100.  
  
```  
CREATE SCHEMA Test ;  
GO  
  
CREATE SEQUENCE Test.TestSeq  
    AS int   
    START WITH 125  
    INCREMENT BY 25  
    MINVALUE 100  
    MAXVALUE 200  
    CYCLE  
    CACHE 3  
;  
GO  
```  
  
 O exemplo a seguir altera a sequência TestSeq para ter um intervalo de 0 a 255. A sequência reinicia a série de numeração com 100 e é incrementada em 50 sempre que um número é gerado.  
  
```  
ALTER SEQUENCE Test. TestSeq  
    RESTART WITH 100  
    INCREMENT BY 50  
    MINVALUE 50  
    MAXVALUE 200  
    NO CYCLE  
    NO CACHE  
;  
GO  
```  
  
 Uma vez que a sequência não executará nenhum ciclo, a função **NEXT VALUE FOR** resultará em um erro quando a sequência exceder 200.  
  
### <a name="b-restarting-a-sequence"></a>B. Reiniciando uma sequência  
 O exemplo a seguir cria uma sequência chamada CountBy1. A sequência usa os valores padrão.  
  
```  
CREATE SEQUENCE Test.CountBy1 ;  
```  
  
 Para gerar um valor de sequência, o proprietário executa a seguinte instrução:  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1  
```  
  
 O valor -9.223.372.036.854.775.808 retornado é o menor valor possível para o tipo de dados **bigint**. O proprietário percebe que ele deseja que a sequência seja iniciada com 1, mas que não indicou a cláusula **START WITH** quando criou a sequência. Para corrigir esse erro, o proprietário executa a instrução a seguir.  
  
```  
ALTER SEQUENCE Test.CountBy1 RESTART WITH 1 ;  
```  
  
 Em seguida, o proprietário executa a instrução a seguir novamente para gerar um número de sequência.  
  
```  
SELECT NEXT VALUE FOR Test.CountBy1;  
```  
  
 O número agora é 1, conforme esperado.  
  
 A sequência CountBy1 foi criada usando o valor padrão de NO CYCLE e, por isso, ela deixará de funcionar após gerar o número 9.223.372.036.854.775.807. As chamadas subsequentes para o objeto de sequência retornarão o erro 11728. A instrução a seguir altera o objeto de sequência para executar um ciclo e define um cache de 20.  
  
```  
ALTER SEQUENCE Test.CountBy1  
    CYCLE  
    CACHE 20 ;  
  
```  
  
 Agora, quando o objeto de sequência alcançar 9.223.372.036.854.775.807, ele executará o ciclo e o próximo número após o ciclo será o valor mínimo do tipo de dados, -9.223.372.036.854.775.808.  
  
 O proprietário percebeu que o tipo de dados **bigint** usa 8 bytes sempre que é utilizado. O tipo de dados **int** que usa 4 bytes é suficiente. Entretanto, o tipo de dados de um objeto de sequência não pode ser alterado. Para alterar para um tipo de dados **int**, o proprietário deve remover o objeto de sequência e recriá-lo com o tipo de dados correto.  
  
## <a name="see-also"></a>Consulte Também  
 [CREATE SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/create-sequence-transact-sql.md)   
 [DROP SEQUENCE &#40;Transact-SQL&#41;](../../t-sql/statements/drop-sequence-transact-sql.md)   
 [NEXT VALUE FOR &#40;Transact-SQL&#41;](../../t-sql/functions/next-value-for-transact-sql.md)   
 [Sequence Numbers](../../relational-databases/sequence-numbers/sequence-numbers.md)   
 [sp_sequence_get_range &#40;Transact-SQL&#41;](../../relational-databases/system-stored-procedures/sp-sequence-get-range-transact-sql.md)  
  
  
