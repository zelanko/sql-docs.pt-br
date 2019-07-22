---
title: Índices em colunas computadas | Microsoft Docs
ms.custom: ''
ms.date: 11/19/2018
ms.prod: sql
ms.prod_service: table-view-index, sql-database
ms.reviewer: ''
ms.technology: table-view-index
ms.topic: conceptual
helpviewer_keywords:
- computed columns, index creation
- index creation [SQL Server], computed columns
- imprecise columns
- persisted computed columns
- precise [SQL Server]
ms.assetid: 8d17ac9c-f3af-4bbb-9cc1-5cf647e994c4
author: MikeRayMSFT
ms.author: mikeray
monikerRange: =azuresqldb-current||>=sql-server-2016||=sqlallproducts-allversions||>=sql-server-linux-2017||=azuresqldb-mi-current
ms.openlocfilehash: cf54565115df53dc7d502f48aad68f9974adebd0
ms.sourcegitcommit: b2464064c0566590e486a3aafae6d67ce2645cef
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/15/2019
ms.locfileid: "67909688"
---
# <a name="indexes-on-computed-columns"></a>Índices em colunas computadas
[!INCLUDE[appliesto-ss-asdb-xxxx-xxx-md](../../includes/appliesto-ss-asdb-xxxx-xxx-md.md)]

Você pode definir índices em colunas computadas contanto que os seguintes requisitos sejam satisfeitos:  
  
-   Requisitos de propriedade  
-   Requisitos de determinismo  
-   Requisitos de precisão  
-   Requisitos de tipo de dados  
-   Requisitos de opção SET  
  
#### <a name="ownership-requirements"></a>Requisitos de propriedade
  
Todas as referências de função na coluna computada devem ter o mesmo proprietário da tabela.  
  
## <a name="determinism-requirements"></a>Requisitos de determinismo  

Expressões são determinísticas se elas sempre retornarem o mesmo resultado para um conjunto de entradas especificado. A propriedade **IsDeterministic** da função [COLUMNPROPERTY](../../t-sql/functions/columnproperty-transact-sql.md) relata se um *computed_column_expression* é determinístico.  
A *computed_column_expression* deve ser determinística. Uma *computed_column_expression* é determinística quando todas as seguintes condições são verdadeiras:  
  
-   Todas as funções mencionadas pela expressão são determinísticas e precisas. Essas funções incluem as funções definidas pelo usuário e internas. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../../relational-databases/user-defined-functions/deterministic-and-nondeterministic-functions.md). Funções podem ser imprecisas se a coluna computada for PERSISTED. Para obter mais informações, veja [Criando índices em colunas computadas persistentes](#BKMK_persisted) , mais adiante neste tópico.  
  
-   Todas as colunas mencionadas na expressão vêm da tabela que contém a coluna computada.  
  
-   Nenhuma referência de coluna recebe dados de várias linhas. Por exemplo, funções de agregação como SUM ou AVG dependem de dados de várias linhas e criam uma *computed_column_expression* não determinística.  
  
-   A *computed_column_expression* não tem acesso a dados do sistema nem a dados do usuário.  
  
Qualquer coluna computada que contenha uma expressão CLR (Common Language Runtime) deve ser determinística e marcada como PERSISTED antes que a coluna possa ser indexada. Expressões de tipo de dado CLR definido pelo usuário são permitidas em definições de coluna computada. Colunas computadas cujo tipo é um tipo de dado CLR definido pelo usuário podem ser indexadas contanto que o tipo seja comparável. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../../relational-databases/clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  

#### <a name="cast-and-convert"></a>CAST e CONVERT

Quando você se referir a literais de cadeia de caracteres do tipo de dados de data em colunas computadas indexadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recomendamos que você converta explicitamente o literal para o tipo de data desejado, usando um estilo de formato de data determinístico. Para obter uma lista de estilos de formato de data determinísticos, veja [CAST e CONVERT](../../t-sql/functions/cast-and-convert-transact-sql.md). 

Para obter mais informações, confira [Conversão não determinística de cadeias de caracteres de data literal em valores de DATA](../../t-sql/data-types/nondeterministic-convert-date-literals.md).

#### <a name="compatibility-level"></a>Nível de Compatibilidade

A conversão implícita de dados de caractere não Unicode entre ordenações será considerada não determinística, a menos que o nível de compatibilidade seja definido como 80 ou abaixo disso.  

Quando o nível da configuração da compatibilidade de banco de dados é 90, você não pode criar índices em colunas computadas que contêm essas expressões. Porém, a existência de colunas computadas com essas expressões de um banco de dados atualizado é sustentável. Se você usar colunas computadas indexadas que contêm conversões implícitas de cadeia de caracteres para datas; para evitar possível corrupção de índice, verifique se as configurações LANGUAGE e DATEFORMAT estão consistentes em seus bancos de dados e aplicativos.

O nível de compatibilidade 90 corresponde ao SQL Server 2005.



## <a name="precision-requirements"></a>Requisitos de precisão
  
 A *computed_column_expression* deve ser precisa. Uma *computed_column_expression* é precisa quando uma ou mais das seguintes opções é verdadeira:  
  
-   Não é uma expressão dos tipos de dados **float** ou **real** .  
-   Não usa um tipo de dados **float** ou **real** na definição. Por exemplo, na instrução a seguir, a coluna `y` é **int** e determinística, mas não é precisa.  
  
    ```sql  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
> Qualquer expressão **float** ou **real** é considerada imprecisa e não pode ser uma chave de um índice; uma expressão **float** ou **real** pode ser usada em uma exibição indexada, mas não como uma chave. Isso também é verdade para colunas computadas. Qualquer função, expressão ou função definida pelo usuário será considerada imprecisa se contiver uma expressão **float** ou **real** . Isso inclui as lógicas (comparações).  
  
A propriedade **IsPrecise** da função COLUMNPROPERTY relata se uma *computed_column_expression* é precisa.  


## <a name="data-type-requirements"></a>Requisitos de tipo de dados
  
-   A *computed_column_expression* definida para a coluna computada não pode ser avaliada para os tipos de dados **text**, **ntext**ou **image** .  
-   Colunas computadas derivadas dos tipos de dados **image**, **ntext**, **text**, **varchar(max)** , **nvarchar(max)** , **varbinary(max)** e **xml** podem ser indexadas, desde que o tipo de dados da coluna computada seja permitido como uma coluna de chave de índice.  
-   Colunas computadas derivadas dos tipos de dados **image**, **ntext**e **text** podem ser colunas (incluídas) não chave em um índice não clusterizado, desde que o tipo de dados da coluna computada seja permitida como uma coluna de índice não chave.  


## <a name="set-option-requirements"></a>Requisitos de opção SET
  
-   A opção de nível de conexão ANSI_NULLS deve ser definida como ON quando a instrução CREATE TABLE ou ALTER TABLE que define a coluna computada é executada. A função [OBJECTPROPERTY](../../t-sql/functions/objectproperty-transact-sql.md) relata se a opção está ativa pela propriedade **IsAnsiNullsOn** .  
-   A conexão na qual o índice é criado e todas as conexões que tentam instruções INSERT, UPDATE ou DELETE que alterarão valores no índice, deve ter seis opções de SET definidas como ON e uma opção definida como OFF. O otimizador ignora um índice em uma coluna computada para qualquer instrução SELECT executada por uma conexão que não tenha essas mesmas opções de configuração.  
  
    -   A opção de NUMERIC_ROUNDABORT deve ser definida como OFF e as opções seguintes devem ser definidas como ON:  
    -   ANSI_NULLS  
    -   ANSI_PADDING  
    -   ANSI_WARNINGS  
    -   ARITHABORT  
    -   CONCAT_NULL_YIELDS_NULL  
    -   QUOTED_IDENTIFIER  
  
> [!NOTE]
> A definição de ANSI_WARNINGS como ON definirá ARITHABORT implicitamente como ON quando o nível de compatibilidade do banco de dados estiver definido como 90 ou mais.  
  
## <a name="BKMK_persisted"></a> Criando índices em colunas computadas persistentes  

Às vezes, você pode criar uma coluna computada definida por uma expressão determinística, mas imprecisa. Você pode fazer isso quando a coluna está marcada como PERSISTED na instrução CREATE TABLE ou ALTER TABLE.

Isso significa que o [!INCLUDE[ssDE](../../includes/ssde-md.md)] armazena os valores computados na tabela e os atualiza quando as outras colunas das quais a coluna computada depende são atualizadas. O [!INCLUDE[ssDE](../../includes/ssde-md.md)] usa esses valores persistentes ao criar um índice na coluna e quando o índice é referenciado em uma consulta.

Essa opção permite a você criar um índice em uma coluna computada quando [!INCLUDE[ssDE](../../includes/ssde-md.md)] não puder provar, com exatidão, se uma função que retorna expressões de coluna computada, particularmente uma função CLR que é criada no [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)], é determinística e precisa.  


  
## <a name="related-content"></a>Conteúdo relacionado  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](../../t-sql/functions/columnproperty-transact-sql.md)   
 [CREATE TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/create-table-transact-sql.md)    
 [ALTER TABLE &#40;Transact-SQL&#41;](../../t-sql/statements/alter-table-transact-sql.md)
  
  
