---
title: Trabalhando com tipos de dados R | Microsoft Docs
ms.custom:
- SQL2016_New_Updated
ms.date: 01/31/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- r-services
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: jeannt
ms.author: jeannt
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 96ec352784f060f444b8adcae6005dd454b3b460
ms.openlocfilehash: c4ab2ed64eaaf970057987c7169d12e93c4380ad
ms.contentlocale: pt-br
ms.lasthandoff: 09/27/2017

---
# <a name="r-libraries-and-r-data-types"></a>Tipos de dados de R e bibliotecas de R

Este tópico descreve as bibliotecas de R que estão incluídas e os tipos de dados que têm suporte nos seguintes produtos:

+ SQL Server 2016 R Services (no banco de dados)
+ Serviços (no banco de dados) de aprendizado de máquina do SQL Server

Este tópico também lista os tipos de dados sem suporte e lista o tipo de dados conversões que podem ser realizadas implicitamente quando dados são passados entre R e SQL Server.

## <a name="r-libraries"></a>Bibliotecas de R

Ambos os produtos, serviços de R e serviços de aprendizado de máquina com R, são alinhados com as versões específicas do Microsoft R Open. Por exemplo, a versão mais recente, o SQL Server de 2017 Machine Learning Services baseia-se no Microsoft R Open 3.3.3.

Para exibir a versão de R associada a uma determinada instância do SQL Server, abra RGui.

1. Para a instância padrão, o caminho deverá ser da seguinte maneira:`C:\Program Files\Microsoft SQL Server\MSSQL14.MSSQLSERVER\R_SERVICES\bin\x64\`
2. Será exibida uma mensagem que lista a distribuição de R e o número da versão Microsoft R Open.

Para localizar a versão de R incluída em uma versão específica do Microsoft R Server, consulte [R Server - What's New](https://msdn.microsoft.com/microsoft-r/rserver-whats-new#new-and-updated-packages).

Observe que o sistema de gerenciamento de pacote no SQL Server significa que várias versões de um pacote R podem ser instaladas no mesmo computador, com vários usuários compartilhando o mesmo pacote ou usar versões diferentes do mesmo pacote. Para obter mais informações, consulte [gerenciamento de pacotes de R no SQL Server](../r/r-package-management-for-sql-server-r-services.md).

## <a name="r-and-sql-data-types"></a>Tipos de dados do SQL e R

Enquanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a vários tipos de dados, R tem um número limitado de tipos de dados escalares (numérico, inteiro, complexos, lógicos, caracteres, data/hora e brutos). Como resultado, sempre que você usar dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em scripts de R, dados podem ser convertidos implicitamente em um tipo de dados compatíveis. No entanto, geralmente uma conversão exata não pode ser executada automaticamente e será retornado um erro, como "Tipo de dados do SQL sem tratamento".

Esta seção lista as conversões implícitas que são fornecidas e lista os tipos de dados sem suporte. Orientação é fornecida para o mapeamento de tipos de dados entre R e SQL Server.

## <a name="implicit-data-type-conversions-between-r-and-sql-server"></a>Conversões de tipo de dados implícitos entre R e SQL Server

A tabela a seguir mostra as alterações em tipos de dados e valores quando dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são usados em um script de R e depois retornados ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].

|Tipo SQL|Classe R|Tipo RESULT SET|Comentários|
|-|-|-|-|
|**bigint**|`numeric`|**float**||
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|
|**bit**|`logical`|**bit**||
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||
|**datetime**|`POSIXct`|**datetime**|Representado como GMT|
|**date**|`POSIXct`|**datetime**|Representado como GMT|
|**decimal(p,s)**|`numeric`|**float**||
|**float**|`numeric`|**float**||
|**int**|`integer`|**int**||
|**money**|`numeric`|**float**||
|**numeric(p,s)**|`numeric`|**float**||
|**real**|`numeric`|**float**||
|**smalldatetime**|`POSIXct`|**datetime**|Representado como GMT|
|**smallint**|`integer`|**int**||
|**smallmoney**|`numeric`|**float**||
|**tinyint**|`integer`|**int**||
|**uniqueidentifier**|`character`|**varchar(max)**||
|**varbinary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|
|**varbinary(max)**|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|
|**varchar(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||


## <a name="data-types-not-supported-by-r"></a>Tipos de dados sem suporte em R

Das categorias de tipos de dados com suporte no [sistema de tipos do SQL Server](../../t-sql/data-types/data-types-transact-sql.md), os seguintes tipos provavelmente apresentam problemas quando passados para o código R:

+ Tipos de dados listados no **outros** seção do tópico de sistema de tipo SQL: **cursor**, **timestamp**, **hierarchyid**,  **uniqueidentifier**, **sql_variant**, **xml**, **tabela**
+ Todos os tipos espaciais
+ **image**

## <a name="data-types-that-might-convert-poorly"></a>Tipos de dados que podem ser mal convertidos

+ A maioria dos tipos de data/hora deve funcionar, exceto por **datetimeoffset** 
+ Há suporte para a maioria dos tipos de dados numéricos, mas as conversões podem falhar para **money** e **smallmoney**
+ Há suporte para **varchar**, porém, uma vez que o SQL Server usa Unicode como regra, usar **nvarchar** e outros tipos de dados de texto Unicode é recomendado sempre que possível.
+ Funções da biblioteca RevoScaleR prefixadas com rx podem lidar com os tipos de dados binários do SQL (**binary** e **varbinary**), porém, na maioria dos cenários, será necessário tratamento especial para esses tipos. A maioria dos códigos R não funciona com colunas binárias.

  
 Para obter mais informações sobre os tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], veja [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md)

## <a name="changes-in-data-types-between-sql-server-2016-and-earlier-versions"></a>Alterações nos tipos de dados entre o SQL Server 2016 e versões anteriores

O Microsoft SQL Server 2016 e o Banco de Dados SQL do Microsoft Azure incluem melhorias em conversões de tipo de dados e em várias outras operações. A maioria dessas melhorias oferece maior precisão ao lidar com tipos de ponto flutuante, bem como alterações secundárias a operações em tipos de **datetime** clássicos.

Esses aprimoramentos estão disponíveis por padrão quando você usa um nível de compatibilidade do banco de dados de 130 ou posterior. No entanto, se você usar um nível de compatibilidade diferentes ou conectar-se a um banco de dados usando uma versão mais antiga, poderá ver diferenças na precisão dos números ou outros resultados. 

Para obter mais informações, consulte [SQL Server 2016: melhorias no tratamento de alguns tipos de dados e operações incomuns](https://support.microsoft.com/help/4010261/sql-server-2016-improvements-in-handling-some-data-types-and-uncommon-).
 

## <a name="verify-r-and-sql-data-schemas-in-advance"></a>Verifique esquemas de dados SQL e R com antecedência 

Em geral, sempre que você tiver alguma dúvida sobre como uma estrutura de dados ou um tipo de dados específico está sendo usado em R, use a função  `str()` para obter a estrutura interna e o tipo do objeto R. O resultado da função é impresso no console de R e também está disponível nos resultados da consulta, na guia **Mensagens** em [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)]. 

Ao recuperar dados de um banco de dados para uso em código R, você sempre deve eliminar colunas que não possam ser usadas em R, bem como colunas que não sejam úteis para análise, como GUIDS (identificador exclusivo), carimbos de data/hora e outras colunas usadas para auditoria ou informações de linhagem criadas pelos processos de ETL. 

Observe que incluir colunas desnecessárias pode reduzir significativamente o desempenho do código R, especialmente se colunas de alta cardinalidade forem usadas como fatores. Portanto, é recomendável usar os procedimentos armazenados do sistema do SQL Server e modos de exibição de informações para obter os tipos de dados para uma determinada tabela com antecedência e eliminar ou converter as colunas incompatíveis. Para obter mais informações, consulte [Exibições do esquema de informações em Transact-SQL](../../relational-databases/system-information-schema-views/system-information-schema-views-transact-sql.md)

Se R não der suporte para um determinado tipo de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], mas você precisar usar as colunas de dados no script de R, será recomendável usar as funções [CAST and CONVERT &#40;Transact-SQL&#41;](../../t-sql/functions/cast-and-convert-transact-sql.md) para garantir que as conversões de tipo de dados sejam executadas conforme o esperado antes de usar os dados no script de R.  

> [!WARNING]
Se você usar o **rxDataStep** para remover colunas incompatíveis durante a movimentação de dados, lembre-se de que os argumentos _varsToKeep_ e _varsToDrop_ não dão suporte para o tipo de fonte de dados **RxSqlServerData**.


## <a name="examples"></a>Exemplos

### <a name="example-1-implicit-conversion"></a>Exemplo 1: conversão implícita

O exemplo a seguir demonstra como os dados são transformados ao fazer a viagem de ida e volta entre SQL Server e R.

A consulta obtém uma série de valores de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tabela e usa o procedimento armazenado [sp_execute_external_script](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para gerar os valores usando o tempo de execução de R.

```SQL
CREATE TABLE MyTable (    
 c1 int,    
 c2 varchar(10),    
 c3 uniqueidentifier    
);    
go    
INSERT MyTable VALUES(1, 'Hello', newid());    
INSERT MyTable VALUES(-11, 'world', newid());    
SELECT * FROM MyTable;    
  
EXECUTE sp_execute_external_script    
 @language = N'R'    
 , @script = N'    
inputDataSet["cR"] <- c(4, 2)    
str(inputDataSet)    
outputDataSet <- inputDataSet'    
 , @input_data_1 = N'SELECT c1, c2, c3 FROM MyTable'    
 , @input_data_1_name = N'inputDataSet'    
 , @output_data_1_name = N'outputDataSet'    
 WITH RESULT SETS((C1 int, C2 varchar(max), C3 varchar(max), C4 float));  
```

**Resultados**

||||||
|-|-|-|-|-|
||C1|C2|C3|C4|
|1|1|Hello|6e225611-4b58-4995-a0a5-554d19012ef1|4|
|1|-11|world|6732ea46-2d5d-430b-8ao1-86e7f3351c3e|2|

Observe o uso da função `str` em R para obter o esquema dos dados de saída. A função retorna as seguintes informações:

<code>'data.frame':2 obs. of  4 variables:</code>
<code> $ c1: int  1 -11</code>
<code> $ c2: Factor w/ 2 levels "Hello","world": 1 2</code>
<code> $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1</code>
<code> $ cR: num  4 2</code>

A partir disso, você pode ver que as seguintes conversões de tipo de dados foram realizadas implicitamente como parte dessa consulta:

-   **Coluna C1**. A coluna é representada como **int** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` em R, e **int** no conjunto de resultados de saída.  
  
     Nenhuma conversão de tipo foi realizada.  
  
-   **Coluna C2**. A coluna é representada como **varchar(10)** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` em R, e **varchar(max)** na saída.  
  
     Observe como a saída muda; qualquer cadeia de caracteres de R (um fator ou uma cadeia de caracteres regular) será representada como **varchar(max)**, não importa o comprimento das cadeias de caracteres.  
  
-   **Coluna C3**.  A coluna é representada como **uniqueidentifier** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` em R, e **varchar(max)** na saída.
  
     Observe a conversão de tipo de dados que acontece. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a **uniqueidentifier** mas R não; portanto, os identificadores são representados como cadeias de caracteres.
  
-   **Coluna C4**. A coluna contém valores gerados pelo script de R e não presentes nos dados originais.


## <a name="example-2-dynamic-column-selection-using-r"></a>Exemplo 2: Seleção de coluna dinâmica usando R

O exemplo a seguir mostra como você pode usar o código R para verificar tipos de coluna inválidos. Obtém o esquema de uma tabela especificada usando o sistema do SQL Server exibe e remove quaisquer colunas que tenham um tipo inválido especificado.

```R
connStr <- "Server=.;Database=TestDB;Trusted_Connection=Yes"
data <- RxSqlServerData(connectionString = connStr, sqlQuery = "SELECT COLUMN_NAME FROM TestDB.INFORMATION_SCHEMA.COLUMNS WHERE TABLE_NAME = N'testdata' AND DATA_TYPE <> 'image';")
columns <- rxImport(data)
columnList <- do.call(paste, c(as.list(columns$COLUMN_NAME), sep = ","))
sqlQuery <- paste("SELECT", columnList, "FROM testdata")
```

## <a name="see-also"></a>Consulte também

[Bibliotecas de Python e tipos de dados](../python/python-libraries-and-data-types.md)

