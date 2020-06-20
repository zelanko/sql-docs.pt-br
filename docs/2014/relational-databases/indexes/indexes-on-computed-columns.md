---
title: Índices em colunas computadas | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
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
ms.openlocfilehash: 2ecbca9e7838c4c9395a8bcb6e11351c40f7037f
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85049889"
---
# <a name="indexes-on-computed-columns"></a>Índices em colunas computadas
  Você pode definir índices em colunas computadas contanto que os seguintes requisitos sejam satisfeitos:  
  
-   Requisitos de propriedade  
  
-   Requisitos de determinismo  
  
-   Requisitos de precisão  
  
-   Requisitos de tipo de dados  
  
-   Requisitos de opção SET  
  
 **Ownership Requirements**  
  
 Todas as referências de função na coluna computada devem ter o mesmo proprietário da tabela.  
  
 **Determinism Requirements**  
  
> [!IMPORTANT]  
>  Expressões são determinísticas se elas sempre retornarem o mesmo resultado para um conjunto de entradas especificado. A propriedade **IsDeterministic** da função [COLUMNPROPERTY](/sql/t-sql/functions/columnproperty-transact-sql) relata se um *computed_column_expression* é determinístico.  
  
 A *computed_column_expression* deve ser determinística. Uma *computed_column_expression* é determinística quando uma ou mais das seguintes opções é verdadeira:  
  
-   Todas as funções mencionadas pela expressão são determinísticas e precisas. Essas funções incluem as funções definidas pelo usuário e internas. Para obter mais informações, veja [Funções determinísticas e não determinísticas](../user-defined-functions/deterministic-and-nondeterministic-functions.md). Funções podem ser imprecisas se a coluna computada for PERSISTED. Para obter mais informações, veja [Criando índices em colunas computadas persistentes](#BKMK_persisted) , mais adiante neste tópico.  
  
-   Todas as colunas mencionadas na expressão vêm da tabela que contém a coluna computada.  
  
-   Nenhuma referência de coluna recebe dados de várias linhas. Por exemplo, funções de agregação como SUM ou AVG dependem de dados de várias linhas e criam uma *computed_column_expression* não determinística.  
  
-   A *computed_column_expression* não tem acesso a dados do sistema nem a dados do usuário.  
  
 Qualquer coluna computada que contenha uma expressão CLR (Common Language Runtime) deve ser determinística e marcada como PERSISTED antes que a coluna possa ser indexada. Expressões de tipo de dado CLR definido pelo usuário são permitidas em definições de coluna computada. Colunas computadas cujo tipo é um tipo de dado CLR definido pelo usuário podem ser indexadas contanto que o tipo seja comparável. Para obter mais informações, veja [Tipos CLR definidos pelo usuário](../clr-integration-database-objects-user-defined-types/clr-user-defined-types.md).  
  
> [!NOTE]  
>  Quando você se referir a literais de cadeia de caracteres do tipo de dados de data em colunas computadas indexadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], recomendamos que você converta explicitamente o literal para o tipo de data desejado, usando um estilo de formato de data determinístico. Para obter uma lista de estilos de formato de data determinísticos, veja [CAST e CONVERT](/sql/t-sql/functions/cast-and-convert-transact-sql). Expressões que envolvem conversão implícita de cadeias de caracteres para tipos de dados de data são consideradas não determinísticas, a menos que o nível de compatibilidade de banco de dados seja definido como 80 ou abaixo disso. Isso ocorre porque os resultados dependem das configurações de [LANGUAGE](/sql/t-sql/statements/set-language-transact-sql) e [DATEFORMAT](/sql/t-sql/statements/set-dateformat-transact-sql) da sessão de servidor. Por exemplo, os resultados da expressão `CONVERT (datetime, '30 listopad 1996', 113)` dependem da configuração LANGUAGE porque a cadeia de caracteres '`30 listopad 1996`' significa meses diferentes em idiomas. Semelhantemente, na expressão `DATEADD(mm,3,'2000-12-01')`, o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] interpreta a cadeia de caracteres `'2000-12-01'` com base na configuração DATEFORMAT.  
>   
>  A conversão implícita de dados de caracteres não Unicode entre ordenações também é considerada não determinística, a menos que o nível de compatibilidade seja definido como 80 ou abaixo disso.  
>   
>  Quando o nível da configuração da compatibilidade de banco de dados é 90, você não pode criar índices em colunas computadas que contêm essas expressões. Porém, a existência de colunas computadas com essas expressões de um banco de dados atualizado é sustentável. Se você usar colunas computadas indexadas que contêm conversões implícitas de cadeia de caracteres para datas; para evitar possível corrupção de índice, verifique se as configurações LANGUAGE e DATEFORMAT estão consistentes em seus bancos de dados e aplicativos.  
  
 **Precision Requirements**  
  
 A *computed_column_expression* deve ser precisa. Uma *computed_column_expression* é precisa quando uma ou mais das seguintes opções é verdadeira:  
  
-   Não é uma expressão de tipos de dados `float` ou `real`.  
  
-   Não usa `float` ou tipo de dados `real` em sua definição. Por exemplo, na instrução a seguir, a coluna `y` é `int` e determinística mas não é precisa.  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  Qualquer expressão `float` ou `real` é considerada imprecisa e não pode ser uma chave de um índice; uma expressão `float` ou `real` pode ser usada em uma exibição indexada mas não como uma chave. Isso também é verdade para colunas computadas. Qualquer função, expressão, ou função definida pelo usuário será considerada imprecisa se contiver qualquer expressão `float` ou `real`. Isso inclui as lógicas (comparações).  
  
 A propriedade **IsPrecise** da função COLUMNPROPERTY relata se uma *computed_column_expression* é precisa.  
  
 **Data Type Requirements**  
  
-   A *computed_column_expression* definida para a coluna computada não pode ser avaliada como os `text` `ntext` tipos de dados, ou `image` .  
  
-   Colunas computadas derivadas de `image`, `ntext`, `text`, `varchar(max)`, `nvarchar(max)`, `varbinary(max)`, e tipos de dados `xml` podem ser indexados contanto que o tipo de dados de coluna computada seja permitido como coluna de índice chave.  
  
-   Colunas computadas derivadas de `image`, `ntext`, e tipos de dados `text` podem ser colunas não chave (inclusas) em um índice não clusterizado contanto que o tipo de dados da coluna computada seja permitida como coluna de índice não chave.  
  
 **Requisitos de opção SET**  
  
-   A opção de nível de conexão ANSI_NULLS deve ser definida como ON quando a instrução CREATE TABLE ou ALTER TABLE que define a coluna computada é executada. A função [OBJECTPROPERTY](/sql/t-sql/functions/objectpropertyex-transact-sql) relata se a opção está ativa pela propriedade **IsAnsiNullsOn** .  
  
-   A conexão na qual o índice é criado e todas as conexões que tentam instruções INSERT, UPDATE ou DELETE que alterarão valores no índice, deve ter seis opções de SET definidas como ON e uma opção definida como OFF. O otimizador ignora um índice em uma coluna computada para qualquer instrução SELECT executada por uma conexão que não tenha essas mesmas opções de configuração.  
  
    -   A opção de NUMERIC_ROUNDABORT deve ser definida como OFF e as opções seguintes devem ser definidas como ON:  
  
    -   ANSI_NULLS  
  
    -   ANSI_PADDING  
  
    -   ANSI_WARNINGS  
  
    -   ARITHABORT  
  
    -   CONCAT_NULL_YIELDS_NULL  
  
    -   QUOTED_IDENTIFIER  
  
     A definição de ANSI_WARNINGS como ON definirá ARITHABORT implicitamente como ON quando o nível de compatibilidade do banco de dados estiver definido como 90 ou mais.  
  
##  <a name="creating-indexes-on-persisted-computed-columns"></a><a name="BKMK_persisted"></a> Criando índices em colunas computadas persistentes  
 Você pode criar um índice em uma coluna computada que está definida com uma expressão determinística, mas imprecisa, se a coluna for marcada como PERSISTED na instrução CREATE TABLE ou ALTER TABLE. Isso significa que o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] usa esses valores persistentes ao criar um índice na coluna e quando o índice é referenciado em uma consulta. Essa opção permite que você crie um índice em uma coluna computada quando [!INCLUDE[ssDE](../../../includes/dnprdnshort-md.md)] , é determinístico e preciso.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)  
  
  
