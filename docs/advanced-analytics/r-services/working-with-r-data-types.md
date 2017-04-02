---
title: "Trabalhando com tipos de dados R | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "r-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 5df99e1c-a89a-42c1-9d68-ffe8d9577c94
caps.latest.revision: 16
author: "jeannt"
ms.author: "jeannt"
manager: "jhubbard"
caps.handback.revision: 12
---
# Trabalhando com tipos de dados R
  Enquanto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a vários tipos de doze dados R tem um número limitado de tipos de dados escalares (numérico, inteiro, complexas, lógica, caracteres, data/hora e raw). Portanto, quando você usa dados de  [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em scripts de R, várias coisas podem acontecer:  
  
-   Os dados são convertidos implicitamente em um tipo de dados compatível.  
  
-   Os dados não podem ser convertidos implicitamente e um erro é retornado.  
  
 Em geral, sempre que você tiver alguma dúvida sobre como uma estrutura de dados ou tipo de dados específico está sendo usada em R, use o  `str()` função para obter a estrutura interna e o tipo do objeto R. O resultado da função é impresso no console de R e também está disponível nos resultados da consulta, no **mensagens** guia [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)].  
  
 Se um determinado [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] não há suporte para tipo de dados R, mas você precisa usar as colunas de dados no script R, é recomendável que você use o [CAST e CONVERT & #40. O Transact-SQL e 41;](../../t-sql/functions/cast-and-convert-transact-sql.md) funções para garantir que os dados de conversões de tipo são executadas conforme o esperado antes de usar os dados em seu script R.  
  
 Para obter mais informações sobre [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] tipos de dados, consulte [tipos de dados e 40; O Transact-SQL e 41;](../../t-sql/data-types/data-types-transact-sql.md)  
  
## Conversão de tipo de dados entre R e SQL Server  
 A tabela a seguir mostra as alterações em tipos de dados e valores quando dados de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é usado em um script de R e, em seguida, retornado ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|||||  
|-|-|-|-|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Tipo|Classe R|Digite **conjunto de resultados**|Comentários|  
|**smalldatetime**|`POSIXct`|**datetime**|Representado como GMT|  
|**smallmoney**|`numeric`|**float**||  
|**datetime**|`POSIXct`|**datetime**|Representado como GMT|  
|**money**|`numeric`|**float**||  
|**uniqueidentifier**|`character`|**varchar(max)**||  
|**numeric(p,s)**|`numeric`|**float**||  
|**decimal(p,s)**|`numeric`|**float**||  
|**date**|`POSIXct`|**datetime**|Representado como GMT|  
|**tinyint**|`integer`|**int**||  
|**bit**|`logical`|**bit**||  
|**smallint**|`integer`|**int**||  
|**int**|`integer`|**int**||  
|**float**|`numeric`|**float**||  
|**real**|`numeric`|**float**||  
|**bigint**|`numeric`|**float**||  
|**binary(n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|  
|**char(n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary (n)**<br /><br /> n <= 8000|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|  
|**varchar (n)**<br /><br /> n <= 8000|`character`|**varchar(max)**||  
|**varbinary(max)**|`raw`|**varbinary(max)**|Só é permitido como parâmetro de entrada e saída|  
  
## Exemplos de conversão de tipo de dados  
 A consulta a seguir obtém uma série de valores de um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da tabela e usa o procedimento armazenado  [sp_execute_external_script & #40. O Transact-SQL e 41;](../../relational-databases/system-stored-procedures/sp-execute-external-script-transact-sql.md) para gerar os valores usando o tempo de execução de R.  
  
```  
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
  
 Observe o uso do `str` função em R para obter o esquema dos dados de saída. A função retorna as seguintes informações:  
  
```  
'data.frame':2 obs. of  4 variables:   
 $ c1: int  1 -11   
 $ c2: Factor w/ 2 levels "Hello","world": 1 2   
 $ c3: Factor w/ 2 levels "6732EA46-2D5D-430B-8A01-86E7F3351C3E",..: 2 1   
 $ cR: num  4 2  
```  
  
 A partir disso, você pode ver que as seguintes conversões de tipo de dados foram realizadas implicitamente como parte dessa consulta:  
  
-   **Coluna C1**. A coluna é representada como **int** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `integer` em R, e **int** no conjunto de resultados de saída.  
  
     Nenhuma conversão de tipo foi realizada.  
  
-   **Coluna C2**. A coluna é representada como **varchar (10)** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `factor` em R, e **varchar (max)** na saída.  
  
     Observe como a saída muda; qualquer cadeia de caracteres de R (um fator ou uma cadeia de caracteres regular) será representada como **varchar (max)**, não importa o que é o comprimento das cadeias de caracteres.  
  
-   **Coluna C3**.  A coluna é representada como **uniqueidentifier** em [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], `character` em R, e **varchar (max)** na saída.  
  
     Observe a conversão de tipo de dados que acontece. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] oferece suporte a **uniqueidentifier** mas R não; portanto, os identificadores são representados como cadeias de caracteres.  
  
-   **Coluna C4**. A coluna contém valores gerados pelo script de R e não presentes nos dados originais.  
 
 ## Consulte também
 [Recursos e tarefas do SQL Server R Services](../../advanced-analytics/r-services/sql-server-r-services-features-and-tasks.md)
  
  