---
title: Retornando a matriz de parâmetros de procedimentos armazenados | Microsoft Docs
ms.custom: ''
ms.date: 01/19/2017
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- stored procedures [ODBC], ODBC driver for Oracle
- ODBC driver for Oracle [ODBC], stored procedures
ms.assetid: 2018069b-da5d-4cee-a971-991897d4f7b5
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: a154a8739438b76f12e311d0dec0e9d98d886457
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63127995"
---
# <a name="returning-array-parameters-from-stored-procedures"></a>Retornar os parâmetros de matriz de procedimentos armazenados
> [!IMPORTANT]  
>  Este recurso será removido em uma versão futura do Windows. Evite usar esse recurso em desenvolvimentos novos e planeje modificar os aplicativos que atualmente o utilizam. Em vez disso, use o driver ODBC fornecido pela Oracle.  
  
 Oracle 7.3, não há nenhuma maneira de acessar um tipo de registro de PL/SQL, exceto a partir de um programa de PL/SQL. Se uma função ou procedimento empacotado tem um argumento formal definido como um tipo de registro de PL/SQL, não é possível associar o argumento formal como um parâmetro. Use o tipo de tabela de PL/SQL no Microsoft ODBC Driver for Oracle para invocar os parâmetros da matriz de procedimentos que contém as sequências de escape corretos.  
  
 Para invocar o procedimento, use a seguinte sintaxe:  
  
```  
{call  <package-name>.<proc-or-func>;  
(..., {resultset <max-records-requested> ,<formal-array-param_1>,;  
 <formal-array-param_2>,...,<formal-array-param_n> }, ... ) }  
```  
  
> [!NOTE]  
>  O \<solicitado de registros de max > parâmetro deve ser maior que ou igual ao número de linhas presentes no conjunto de resultados. Caso contrário, o Oracle retornará um erro que é passado para o usuário pelo driver.  
>   
>  Registros de PL/SQL não podem ser usados como parâmetros de matriz. Cada parâmetro de matriz pode representar apenas uma coluna de uma tabela de banco de dados.  
  
 O exemplo a seguir define um pacote que contém dois procedimentos que retornam conjuntos de resultados diferentes e, em seguida, fornece duas maneiras de retornar conjuntos de resultados do pacote.  
  
## <a name="package-definition"></a>Definição de pacote:  
  
```  
CREATE OR REPLACE PACKAGE SimplePackage AS  
  
TYPE t_id is TABLE of  NUMBER(5)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Course is TABLE of VARCHAR2(10)  
    INDEX BY BINARY_INTEGER;  
  
TYPE t_Dept is TABLE of VARCHAR2(5)  
    INDEX BY BINARY_INTEGER;  
  
PROCEDURE proc1  
   (  
   o_id             OUT    t_id,  
   ao_course       OUT    t_Course,  
   ao_dept         OUT    t_Dept  
   );  
  
TYPE t_pk1Type1 IS TABLE OF VARCHAR2(100) INDEX BY BINARY_INTEGER;  
TYPE t_pk1Type2 IS TABLE OF NUMBER INDEX BY BINARY_INTEGER;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   );  
  
END SimplePackage;  
  
CREATE OR REPLACE PACKAGE BODY SimplePackage AS  
    PROCEDURE  proc1 ( o_id OUT t_id,  
    ao_course OUT t_Course, ao_dept OUT t_Dept   ) AS  
    BEGIN  
          o_id(1):= 200;  
          ao_course(1) :=  'M101';  
          ao_dept(1) :=  'EEE' ;  
  
          o_id(2) := 201;  
          ao_course(2) :=  'PHY320';  
          ao_dept(2) :=  'ECE' ;  
  
     END proc1;  
PROCEDURE proc2  
   (  
   i_Arg1         IN    NUMBER,  
   ao_Arg2         OUT   t_pk1Type1,  
   ao_Arg3         OUT   t_pk1Type2  
   )  
AS  
   i   NUMBER;  
BEGIN  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg2(i) := 'Row Number ' || to_char(i);  
   END LOOP;  
   FOR i IN 1 .. i_Arg1 LOOP  
      ao_Arg3(i) := i;  
   END LOOP;  
END proc2;  
END SimplePackage;  
```  
  
#### <a name="to-invoke-procedure-proc1"></a>Para invocar o procedimento PROC1  
  
1.  Retorne todas as colunas em um único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset  3, o_id , ao_course, ao_dept  } ) }  
    ```  
  
2.  Retorne cada coluna como um único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc1( {resultset 3, o_id},  {resultset 3, ao_course}, {resultset 3, ao_dept} ) }  
    ```  
  
     Isso retorna três conjuntos de resultados, uma para cada coluna.  
  
#### <a name="to-invoke-procedure-proc2"></a>Para invocar o procedimento PROC2  
  
1.  Retorne todas as colunas em um único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset  5, ao_Arg2, ao_Arg3} ) }  
    ```  
  
2.  Retorne cada coluna como um único conjunto de resultados:  
  
    ```  
    {call SimplePackage.Proc2( 5 , {resultset 5, ao_Arg2}, {resultset 5, ao_Arg3} ) }  
    ```  
  
 Certifique-se de que seus aplicativos buscar todos os conjuntos de resultados usando o [SQLMoreResults](../../odbc/microsoft/level-2-api-functions-odbc-driver-for-oracle.md) API. Para obter mais informações, consulte o *referência do programador de ODBC*.  
  
> [!NOTE]  
>  No Driver ODBC para Oracle da versão 2.0, as funções do Oracle que retornam matrizes de PL/SQL não podem ser usadas para retornar conjuntos de resultados.
