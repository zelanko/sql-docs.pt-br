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
manager: craigg
ms.openlocfilehash: c5aa2bd118d99afea6a1ee6ea8f41c646146c32f
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48049566"
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
>  A conversão implícita de dados de caracteres não Unicode entre agrupamentos também é considerada não determinística, a menos que o nível de compatibilidade seja definido como 80 ou abaixo disso.  
>   
>  Quando o nível da configuração da compatibilidade de banco de dados é 90, você não pode criar índices em colunas computadas que contêm essas expressões. Porém, a existência de colunas computadas com essas expressões de um banco de dados atualizado é sustentável. Se você usar colunas computadas indexadas que contêm conversões implícitas de cadeia de caracteres para datas; para evitar possível corrupção de índice, verifique se as configurações LANGUAGE e DATEFORMAT estão consistentes em seus bancos de dados e aplicativos.  
  
 **Precision Requirements**  
  
 A *computed_column_expression* deve ser precisa. Uma *computed_column_expression* é precisa quando uma ou mais das seguintes opções é verdadeira:  
  
-   Não é uma expressão de tipos de dados `float` ou `real`.  
  
-   Ele não usa um `float` ou `real` tipo de dados em sua definição. Por exemplo, na instrução a seguir, coluna `y` é `int` e determinística mas não precisa.  
  
    ```  
    CREATE TABLE t2 (a int, b int, c int, x float,   
       y AS CASE x   
             WHEN 0 THEN a   
             WHEN 1 THEN b   
             ELSE c   
          END);  
    ```  
  
> [!NOTE]  
>  Qualquer `float` ou `real` expressão é considerada imprecisa e não pode ser uma chave de um índice; uma `float` ou `real` expressão pode ser usada em uma exibição indexada, mas não como uma chave. Isso também é verdade para colunas computadas. Qualquer função, expressão ou função definida pelo usuário será considerada imprecisa se contiver uma `float` ou `real` expressões. Isso inclui as lógicas (comparações).  
  
 A propriedade **IsPrecise** da função COLUMNPROPERTY relata se uma *computed_column_expression* é precisa.  
  
 **Data Type Requirements**  
  
-   O *computed_column_expression* definido para a coluna computada não pode ser avaliada como o `text`, `ntext`, ou `image` tipos de dados.  
  
-   Colunas computadas derivadas dos `image`, `ntext`, `text`, `varchar(max)`, `nvarchar(max)`, `varbinary(max)`, e `xml` tipos de dados podem ser indexados, desde que o tipo de dados de coluna computada seja permitido como uma coluna de chave de índice.  
  
-   Colunas computadas derivadas dos `image`, `ntext`, e `text` tipos de dados podem ser colunas (incluídas) em um índice não clusterizado, desde que o tipo de dados de coluna computada seja permitido como uma coluna de índice não chave.  
  
 **SET Option Requirements**  
  
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
  
##  <a name="BKMK_persisted"></a> Criando índices em colunas computadas persistentes  
 Você pode criar um índice em uma coluna computada que está definida com uma expressão determinística, mas imprecisa, se a coluna for marcada como PERSISTED na instrução CREATE TABLE ou ALTER TABLE. Isso significa que o [!INCLUDE[ssDE](../../../includes/ssde-md.md)] usa esses valores persistentes quando ele cria um índice na coluna, e quando o índice é referenciado em uma consulta. Essa opção permite que você crie um índice em uma coluna computada quando [!INCLUDE[ssDE](../../../includes/dnprdnshort-md.md)], é determinística e precisa.  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [COLUMNPROPERTY &#40;Transact-SQL&#41;](/sql/t-sql/functions/columnproperty-transact-sql)  
  
  
