---
title: Tamanho da tabela e da linha em tabelas com otimização de memória | Microsoft Docs
ms.custom: ''
ms.date: 10/18/2019
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: in-memory-oltp
ms.topic: conceptual
ms.assetid: b0a248a4-4488-4cc8-89fc-46906a8c24a1
author: MightyPen
ms.author: genemi
manager: craigg
ms.openlocfilehash: c320db0f568b7182a48e5b1719f68d17ade11629
ms.sourcegitcommit: 82a1ad732fb31d5fa4368c6270185c3f99827c97
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/21/2019
ms.locfileid: "72688896"
---
# <a name="table-and-row-size-in-memory-optimized-tables"></a>Tamanho da tabela e da linha em tabelas com otimização de memória
  Uma tabela com otimização de memória consiste em uma coleção de linhas e índices que contêm ponteiros para linhas. Em uma tabela com otimização de memória, as linhas não podem ter mais de 8.060 bytes. Entender o tamanho de uma tabela com otimização de memória ajudará você a entender se o seu computador tem memória suficiente.  
  
 Há dois motivos para calcular o tamanho da tabela e da linha:  
  
-   Qual a quantidade de memória que uma tabela usa?  
  
    -   A quantidade de memória usada pela tabela não pode ser calculada exatamente. Muitos fatores afetam a quantidade de memória usada, Fatores como alocação de memória baseada em página, localidade, cache e preenchimento. Além disso, várias versões de linhas que têm transações ativas associadas ou que estão aguardando a coleta de lixo.  
  
    -   O tamanho mínimo necessário para os dados e índices na tabela é fornecido pelo cálculo para [tamanho da tabela], discutido abaixo.  
  
    -   O cálculo do uso de memória é a melhor aproximação e você é aconselhado a incluir o planejamento de capacidade em seus planos de implantação.  
  
-   O tamanho dos dados de uma linha e ele se ajusta à limitação de tamanho de linha de 8.060 bytes? Para responder a essas perguntas, use a computação para [tamanho do corpo da linha], discutida abaixo.  
  
 A figura a seguir ilustra uma tabela com índices e linhas que, por sua vez, têm cabeçalhos e corpos de linha:  
  
 ![Tabela com otimização de memória.](../../database-engine/media/hekaton-guide-1.gif "Tabela com otimização de memória.")  
Tabela com otimização de memória, que consiste em índices e linhas.  
  
 O tamanho na memória de uma tabela, em bytes, é calculado da seguinte maneira:  
  
```  
[table size] = [size of index 1] + ... + [size of index n] + ([row size] * [row count])  
```  
  
 O tamanho de um índice de hash é fixado no momento da criação da tabela e depende do número real de buckets. O bucket_count especificado com a especificação de índice é arredondado para a potência mais próxima de 2 para obter a [contagem real de buckets]. Por exemplo, se o bucket_count especificado for 100000, o [contagem de buckets real] para o índice será 131072.  
  
```  
[hash index size] = 8 * [actual bucket count]  
```  
  
 O tamanho da linha é calculado adicionando-se o cabeçalho e o corpo:  
  
```  
[row size] = [row header size] + [actual row body size]  
[row header size] = 24 + 8 * [number of indices]  
```  
  
 **Tamanho do corpo da linha**  
  
 O cálculo de [tamanho do corpo da linha] é abordado na tabela a seguir.  
  
 Há dois cálculos diferentes para o tamanho do corpo da linha: tamanho computado e tamanho real:  
  
-   O tamanho calculado, indicado com [tamanho do corpo da linha computado], é usado para determinar se a limitação de tamanho de linha de 8.060 bytes foi excedida.  
  
-   O tamanho real, indicado com [tamanho real do corpo da linha], é o tamanho real do armazenamento do corpo da linha na memória e nos arquivos de ponto de verificação.  
  
 Ambos [tamanho do corpo da linha computado] e [tamanho real do corpo da linha] são calculados da mesma forma. A única diferença é o cálculo do tamanho das colunas (n) varchar (i) e varbinary (i), conforme refletido na parte inferior da tabela a seguir. O tamanho do corpo da linha calculado usa o tamanho declarado *i* como o tamanho da coluna, enquanto o tamanho do corpo da linha real usa o tamanho real dos dados.  
  
 A tabela a seguir descreve o cálculo do tamanho do corpo da linha, dado como [tamanho real do corpo da linha] = SUM ([tamanho dos tipos superficiais]) + 2 + 2 * [número de colunas de tipo profundas].  
  
|Section|Tamanho|Feitos|  
|-------------|----------|--------------|  
|Colunas do tipo superficial|SUM ([tamanho dos tipos superficiais])<br /><br /> **O tamanho dos tipos individuais é o seguinte:**<br /><br /> Bit &#124; 1<br /><br /> Tinyint &#124; 1<br /><br /> Smallint &#124; 2<br /><br /> Int &#124; 4<br /><br /> Real &#124; 4<br /><br /> Smalldatetime &#124; 4<br /><br /> Smallmoney &#124; 4<br /><br /> Bigint &#124; 8<br /><br /> Datetime &#124; 8<br /><br /> Datetime2 &#124; 8<br /><br /> Float 8<br /><br /> Money 8<br /><br /> Numeric (precisão < = 18) &#124; 8<br /><br /> Time &#124; 8<br /><br /> Numeric (precisão > 18) &#124; 16<br /><br /> Uniqueidentifier &#124; 16||  
|Preenchimento de coluna superficial|Os valores possíveis são:<br /><br /> 1 se houver colunas de tipo profundas e o tamanho total dos dados das colunas superficiais for como um número ímpar.<br /><br /> caso contrário, 0|Os tipos profundos são os tipos (var) binário e (n) (var) Char.|  
|Matriz de deslocamento para colunas do tipo profundas|Os valores possíveis são:<br /><br /> 0 se não houver nenhuma coluna de tipo profunda<br /><br /> 2 + 2 * [número de colunas de tipo profunda] caso contrário|Os tipos profundos são os tipos (var) binário e (n) (var) Char.|  
|Matriz nula|[número de colunas anuláveis]/8, arredondado para bytes completos.|A matriz tem um bit por coluna que permite valor nulo. Isso é arredondado para bytes completos.|  
|Preenchimento de matriz nulo|Os valores possíveis são:<br /><br /> 1 se houver colunas de tipo profundas e o tamanho da matriz NULL for um número ímpar de bytes.<br /><br /> caso contrário, 0|Os tipos profundos são os tipos (var) binário e (n) (var) Char.|  
|Preenchimento|Se não houver nenhuma coluna de tipo profunda: 0<br /><br /> Se houver colunas de tipo profundas, serão adicionados 0-7 bytes de preenchimento, com base no maior alinhamento exigido por uma coluna superficial. Cada coluna superficial requer alinhamento igual ao seu tamanho, conforme documentado acima, exceto que as colunas GUID precisam de alinhamento de 1 byte (e não 16) e colunas numéricas sempre precisam de alinhamento de 8 bytes (nunca 16). O maior requisito de alinhamento entre todas as colunas superficiais é usado e 0-7 bytes de preenchimento são adicionados de forma que o tamanho total até o momento (sem as colunas de tipo profunda) seja um múltiplo do alinhamento necessário.|Os tipos profundos são os tipos (var) binário e (n) (var) Char.|  
|Colunas de tipo profundas de comprimento fixo|SUM ([tamanho das colunas do tipo profundas de comprimento fixo])<br /><br /> O tamanho de cada coluna é o seguinte:<br /><br /> i para char (i) e binary (i).<br /><br /> 2 * i para nchar (i)|As colunas de tipo profundas de comprimento fixo são colunas do tipo Char (i), nchar (i) ou binary (i).|  
|Colunas do tipo profundas de comprimento variável [tamanho calculado]|SUM ([tamanho calculado de colunas do tipo profundas de comprimento variável])<br /><br /> O tamanho calculado de cada coluna é o seguinte:<br /><br /> i para varchar (i) e varbinary (i)<br /><br /> 2 * i para nvarchar (i)|Esta linha é aplicada somente ao [tamanho do corpo da linha computado].<br /><br /> As colunas de tipo profundas de comprimento variável são colunas do tipo varchar (i), nvarchar (i) ou varbinary (i). O tamanho calculado é determinado pelo comprimento máximo (i) da coluna.|  
|Colunas de tipo profundas de comprimento variável [tamanho real]|SUM ([tamanho real de colunas do tipo profundas de comprimento variável])<br /><br /> O tamanho real de cada coluna é o seguinte:<br /><br /> n, em que n é o número de caracteres armazenados na coluna, para varchar (i).<br /><br /> 2 * n, em que n é o número de caracteres armazenados na coluna, para nvarchar (i).<br /><br /> n, em que n é o número de bytes armazenados na coluna, para varbinary (i).|Esta linha é aplicada somente a [tamanho real do corpo da linha].<br /><br /> O tamanho real é determinado pelos dados armazenados nas colunas da linha.|  
  
##  <a name="bkmk_RowStructure"></a>Estrutura de linha  
 As linhas em uma tabela com otimização de memória têm os seguintes componentes:  
  
-   O cabeçalho de linha contém o carimbo de data/hora necessário para implementar o controle de versão de linha. O cabeçalho de linha também contém o ponteiro de índice para implementar o encadeamento de linhas nos buckets de hash (descritos acima).  
  
-   O corpo da linha contém os dados de coluna reais, que incluem algumas informações auxiliares, como a matriz NULL para colunas anuláveis e a matriz offset para tipos de dados de comprimento variável.  
  
 A figura a seguir ilustra a estrutura de linha de uma tabela que tem dois índices:  
  
 ![Estrutura de linha para uma tabela que tem dois índices.](../../database-engine/media/hekaton-tables-4.gif "Estrutura de linha para uma tabela que tem dois índices.")  
  
 Os carimbos de data e hora de início e término indicam o período em que uma determinada versão de linha é válida. As transações que começam nesse intervalo podem ver essa versão de linha. Para obter mais detalhes consulte [Transações em Tabelas com Otimização de Memória](memory-optimized-tables.md).  
  
 Os ponteiros de índice apontam para a próxima linha da cadeia de caracteres que pertence ao bucket de hash. A figura a seguir ilustra a estrutura de uma tabela com duas colunas (nome, cidade) e com dois índices, um no nome da coluna e outro na coluna cidade.  
  
 ![Estrutura de uma tabela com duas colunas e índices.](../../database-engine/media/hekaton-tables-5.gif "Estrutura de uma tabela com duas colunas e índices.")  
  
 Nesta figura, os nomes John e Jane são transformados em hash no primeiro bucket. Janaína tem hash para o segundo Bucket. As cidades Pequim e Bogotá são transformadas em hash no primeiro Bucket. Paris e Praga são codificadas em hash para o segundo Bucket.  
  
 Desse modo, as cadeias do índice de hash na coluna nome são as seguintes:  
  
-   Primeiro Bucket: (João, Pequim); (João, Paris); (Jane, Praga)  
  
-   Segundo bucket: (Susan, Bogotá)  
  
 As cadeias do índice de cidade são as seguintes:  
  
-   Primeiro Bucket: (João, Pequim), (Susan, Bogotá)  
  
-   Segundo bucket: (John, Paris), (Jane, Praga)  
  
 Um carimbo de &#x221e; data/hora final (infinito) indica que esta é a versão válida atualmente da linha. A linha não foi atualizada nem excluída desde que essa versão de linha foi gravada.  
  
 Para um tempo maior que 200, a tabela contém as seguintes linhas:  
  
|Nomes|Azul|  
|----------|----------|  
|João|Pequim|  
|Rosa|Praga|  
  
 No entanto, todas as transações ativas com a hora de início 100 verão a seguinte versão da tabela:  
  
|Nomes|Azul|  
|----------|----------|  
|João|Paris|  
|Rosa|Praga|  
|Susan|Bogata|  
  
##  <a name="bkmk_ExampleComputation"></a>Exemplo: computação de tamanho de tabela e linha  
 Para índices de hash, o número real de buckets é arredondado para a potência mais próxima de 2. Por exemplo, se o bucket_count especificado for 100000, o número real de buckets para o índice será 131072.  
  
 Considere uma tabela Orders com a seguinte definição:  
  
```sql  
CREATE TABLE dbo.Orders (  
     OrderID int NOT NULL   
           PRIMARY KEY NONCLUSTERED,  
     CustomerID int NOT NULL   
           INDEX IX_CustomerID HASH WITH (BUCKET_COUNT=10000),  
     OrderDate datetime NOT NULL,  
     OrderDescription nvarchar(1000)  
) WITH (MEMORY_OPTIMIZED=ON)  
GO  
```  
  
 Observe que essa tabela tem um índice de hash e um índice não clusterizado (a chave primária). Ele também tem três colunas de comprimento fixo e uma coluna de comprimento variável, com uma das colunas sendo anuláveis (OrderDescription). Vamos supor que a tabela Orders tenha 8379 linhas e que o comprimento médio dos valores na coluna OrderDescription seja de 78 caracteres.  
  
 Para determinar o tamanho da tabela, primeiro determine o tamanho dos índices. O bucket_count para ambos os índices é especificado como 10000. Isso é arredondado para a potência mais próxima de 2: 16384. Portanto, o tamanho total dos índices para a tabela Orders é:  
  
```  
8 * 16384 = 131072 bytes  
```  
  
 O que sobra é o tamanho dos dados da tabela, que é  
  
```  
[row size] * [row count] = [row size] * 8379  
```  
  
 (A tabela de exemplo tem 8379 linhas.) Agora, temos:  
  
```  
[row size] = [row header size] + [actual row body size]  
[row header size] = 24 + 8 * [number of indices] = 24 + 8 * 1 = 32 bytes  
```  
  
 Em seguida, vamos calcular [tamanho real do corpo da linha]:  
  
-   Colunas do tipo superficial:  
  
    ```  
    SUM([size of shallow types]) = 4 [int] + 4 [int] + 8 [datetime] = 16  
    ```  
  
-   O preenchimento de coluna superficial é 0, pois o tamanho total da coluna superficial é par.  
  
-   Matriz de deslocamento para colunas do tipo profundas:  
  
    ```  
    2 + 2 * [number of deep type columns] = 2 + 2 * 1 = 4  
    ```  
  
-   Matriz nula = 1  
  
-   Preenchimento de matriz nulo = 1, pois o tamanho da matriz NULL é ímpar e há uma coluna de tipo profunda.  
  
-   Preenchimento  
  
    -   8 é o maior requisito de alinhamento.  
  
    -   O tamanho até o momento é 16 + 0 + 4 + 1 + 1 = 22.  
  
    -   O múltiplo mais próximo de 8 é 24.  
  
    -   O preenchimento total é 24-22 = 2 bytes.  
  
-   Não há colunas de tipo profundas de comprimento fixo (colunas de tipo profundas de comprimento fixo: 0.).  
  
-   O tamanho real da coluna de tipo profunda é 2 * 78 = 156. Uma única coluna do tipo profunda OrderDescription tem o tipo nvarchar.  
  
```  
[actual row body size] = 24 + 156 = 180 bytes  
```  
  
 Para concluir o cálculo:  
  
```  
[row size] = 32 + 180 = 212 bytes  
[table size] = 8 * 16384 + 212 * 8379 = 131072 + 1776348 = 1907420  
```  
  
 O tamanho total da tabela na memória é, portanto, aproximadamente 2 megabytes. Isso não conta com a possível sobrecarga incorrida pela alocação de memória, bem como qualquer controle de versão de linha necessário para as transações que acessam essa tabela.  
  
 A memória real alocada para o e usada por essa tabela e seus índices podem ser obtidas por meio da seguinte consulta:  
  
```sql  
select * from sys.dm_db_xtp_table_memory_stats  
where object_id = object_id('dbo.Orders')  
```  
  
## <a name="see-also"></a>Consulte também  
 [Tabelas com otimização de memória](memory-optimized-tables.md)  
  
  
