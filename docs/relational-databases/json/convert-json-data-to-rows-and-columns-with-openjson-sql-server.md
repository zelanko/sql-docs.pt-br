---
title: "Converter dados JSON em linhas e colunas com OPENJSON (SQL Server) | Microsoft Docs"
ms.custom: 
  - "SQL2016_New_Updated"
ms.date: "01/31/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "dbe-json"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "OPENJSON"
  - "JSON, importando"
  - "Importando JSON"
ms.assetid: 0c139901-01e2-49ef-9d62-57e08e32c68e
caps.latest.revision: 31
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Converter dados JSON em linhas e colunas com OPENJSON (SQL Server)
[!INCLUDE[tsql-appliesto-ss2016-asdb-xxxx-xxx_md](../../includes/tsql-appliesto-ss2016-asdb-xxxx-xxx-md.md)]

  A função de conjunto de linhas **OPENJSON** permite converter texto JSON em um conjunto de linhas e colunas. Você pode usar **OPENJSON** para executar consultas SQL em coleções JSON ou importar texto JSON em tabelas do SQL Server.  
  
> [!NOTE] A função **OPENJSON** está disponível somente no **nível de compatibilidade 130**. Se o nível de compatibilidade do banco de dados for inferior a 130, o SQL Server não poderá localizar e executar a função **OPENJSON**. Outras funções JSON estão disponíveis em todos os níveis de compatibilidade. Você pode verificar o nível de compatibilidade na exibição sys.databases ou nas propriedades do banco de dados.
> 
>   Você pode alterar um nível de compatibilidade do banco de dados usando o seguinte comando:   
>   ALTER DATABASE DatabaseName SET COMPATIBILITY_LEVEL = 130  
  
 A função **OPENJSON** obterá um único objeto JSON ou uma coleção de objetos JSON e vai transformá-las em uma ou várias linhas. Por padrão, a função **OPENJSON** retornará todos os pares de chave: valor que forem encontrados no primeiro nível de objeto JSON ou todos os elementos em matrizes JSON com seus índices.  
  
 Você pode especificar o esquema de linhas que serão retornadas pela função **OPENJSON** usando a cláusula WITH. Esse esquema explícito define a estrutura da saída.  
  
## Usar OPENJSON sem o esquema de resultados

Aqui está um exemplo rápido que usa **OPENJSON** com o esquema padrão e retorna uma linha para cada propriedade do objeto JSON.  
 
Quando você usa a função **OPENJSON** sem esquema especificado de resultados retornados (ou seja, sem cláusula WITH após OPENJSON), a função retorna uma tabela com três colunas: nome da propriedade no objeto de entrada (ou índice do elemento na matriz de entrada), valor da propriedade ou elemento de matriz e o tipo (por exemplo, cadeia de caracteres, número, booliano, matriz ou objeto). Propriedades do objeto JSON (ou elementos de matriz) são retornadas em linhas separadas.  

-   Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema padrão &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-the-default-schema-sql-server.md).
-   Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md). 

```tsql  
SET @json = '{"name":"John","surname":"Doe","age":45,"skills":["SQL","C#","MVC"]}';  
  
SELECT *  
FROM OPENJSON(@json);  
```  
  
**Resultados**  
  
|chave|value|tipo|  
|---------|-----------|----------|  
|name|John|1|  
|sobrenome|Doe|1|  
|idade|45|2|  
|habilidades|["SQL","C#","MVC"]|4|
    
## Usar OPENJSON com um esquema explícito

Aqui está um exemplo rápido que usa **OPENJSON** com um esquema especificado explicitamente.  
  
Quando você especifica o esquema de resultados retornados na cláusula WITH da função **OPENJSON**, a função retorna uma tabela com as colunas que você define na cláusula WITH. Na cláusula WITH, você pode especificar um conjunto de colunas de saída, seus tipos e os caminhos das propriedades de origem de JSON para cada valor de saída. **OPENJSON** será iterado por meio da matriz de objetos JSON, lerá o valor no caminho especificado para cada coluna e converterá o valor para o tipo especificado.  

-   Para obter mais informações e exemplos, consulte [Usar OPENJSON com o esquema explícito &#40;SQL Server&#41;](../../relational-databases/json/use-openjson-with-an-explicit-schema-sql-server.md).
-   Para sintaxe e uso, veja [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md).
  
```tsql  
SET @json =   
 N'[  
      {  
        "Order": {  
          "Number":"SO43659",  
          "Date":"2011-05-31T00:00:00"  
        },  
        "AccountNumber":"AW29825",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":1  
        }  
      },  
      {  
        "Order": {  
          "Number":"SO43661",  
          "Date":"2011-06-01T00:00:00"  
        },  
        "AccountNumber":"AW73565",  
        "Item": {  
          "Price":2024.9940,  
          "Quantity":3  
        }  
     }  
]'  
  
SELECT * FROM  
OPENJSON ( @json )  
WITH (   
             Number   varchar(200) '$.Order.Number' ,  
             Date     datetime     '$.Order.Date',  
             Customer varchar(200) '$.AccountNumber',  
             Quantity int          '$.Item.Quantity'  
)  
```  
  
**Resultados**  
  
|Número|Data|Cliente|Quantidade|  
|------------|----------|--------------|--------------|  
|SO43659|2011-05-31T00:00:00|AW29825|1|  
|SO43661|2011-06-01T00:00:00|AW73565|3|  
  
 Essa função retorna e formata os elementos de uma matriz JSON.  
  
-   Para cada elemento na matriz JSON, **OPENJSON** gera uma nova linha na tabela de saída. Dois elementos na matriz JSON são convertidos em duas linhas na tabela retornada.  
  
-   Para cada coluna, especificada usando a sintaxe `colName type json_path`, a função **OPENJSON** converte o valor encontrado nos elementos de matriz no caminho especificado, converte-os no tipo especificado e preenche uma célula na tabela de saída. Neste exemplo, os valores da coluna Data são obtidos de cada objeto em um caminho `$.Order.Date` e convertidos em valores de data e hora.  
  
Após a transformação da coleção JSON em um conjunto de linhas, você pode executar qualquer consulta SQL nos dados retornados ou inseri-lo em uma tabela.  
  
## Saiba mais sobre o OPENJSON e o suporte interno a JSON no SQL Server  
 [Postagens no blog por Jovan Popovic, gerente de programas da Microsoft](http://blogs.msdn.com/b/sqlserverstorageengine/archive/tags/json/)  
  
## Consulte também  
 [OPENJSON &#40;Transact-SQL&#41;](../../t-sql/functions/openjson-transact-sql.md)  
  
  