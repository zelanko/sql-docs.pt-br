---
title: Tipos de dados PHP padrão
description: Este tópico lista todos os tipos de dados PHP padrão com os tipos de dados do SQL Server correspondentes ao usar o Driver SQLSRV da Microsoft para PHP para SQL Server
ms.custom: ''
ms.date: 08/10/2020
ms.prod: sql
ms.prod_service: connectivity
ms.reviewer: ''
ms.technology: connectivity
ms.topic: conceptual
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
author: David-Engel
ms.author: v-daenge
ms.openlocfilehash: c1e1cf91baf80fd6298eaaca9c9e12a0b5858d9f
ms.sourcegitcommit: d1051f05a7db81ec62d9785bb6af572408f3d4e0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/20/2020
ms.locfileid: "88680783"
---
# <a name="default-php-data-types"></a>Tipos de dados padrão do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ao recuperar dados do servidor, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] converte os dados em um tipo de dados padrão do PHP se nenhum tipo de dados do PHP foi especificado pelo usuário.  
  
Quando dados são retornados usando o driver PDO_SQLSRV, o tipo de dados é int ou cadeia de caracteres.  
  
O restante deste tópico aborda os tipos de dados padrão usando o driver SQLSRV.  
  
A tabela a seguir lista o tipo de dados do SQL Server (o tipo de dados que está sendo recuperado do servidor), o tipo de dados padrão do PHP (o tipo de dados no qual os dados são convertidos) e a codificação padrão para fluxos e cadeias de caracteres. Para obter detalhes sobre como especificar tipos de dados ao recuperar dados do servidor, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
|Tipo do SQL Server|Tipo padrão do PHP|Codificação padrão|  
|-------------------|--------------------|--------------------|  
|BIGINT|String|Caractere de 8 bits<sup>1</sup>|  
|binary|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|bit|Integer|Caractere de 8 bits<sup>1</sup>|  
|char|String|Caractere de 8 bits<sup>1</sup>|  
|date<sup>4</sup>|Datetime|Não aplicável|  
|datetime<sup>4</sup>|Datetime|Não aplicável|  
|datetime2<sup>4</sup>|Datetime|Não aplicável|  
|datetimeoffset<sup>4</sup>|Datetime|Não aplicável|  
|decimal|String|Caractere de 8 bits<sup>1</sup>|  
|FLOAT|Float|Caractere de 8 bits<sup>1</sup>|  
|geografia|Fluxo|Binário<sup>3</sup>|  
|geometria|Fluxo|Binário<sup>3</sup>|  
|image<sup>5</sup>|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|INT|Integer|Caractere de 8 bits<sup>1</sup>|  
|money|String|Caractere de 8 bits<sup>1</sup>|  
|NCHAR|String|Caractere de 8 bits<sup>1</sup>|  
|numeric|String|Caractere de 8 bits<sup>1</sup>|  
|NVARCHAR|String|Caractere de 8 bits<sup>1</sup>|  
|nvarchar(MAX)|Fluxo<sup>2</sup>|Caractere de 8 bits<sup>1</sup>|  
|ntext<sup>6</sup>|Fluxo<sup>2</sup>|Caractere de 8 bits<sup>1</sup>|  
|real|Float|Caractere de 8 bits<sup>1</sup>|  
|smalldatetime|Datetime|Caractere de 8 bits<sup>1</sup>|  
|SMALLINT|Integer|Caractere de 8 bits<sup>1</sup>|  
|SMALLMONEY|String|Caractere de 8 bits<sup>1</sup>|  
|sql_variant<sup>7</sup>|String|Caractere de 8 bits<sup>1</sup>|  
|text<sup>8</sup>|Fluxo<sup>2</sup>|Caractere de 8 bits<sup>1</sup>|  
|time<sup>4</sup>|Datetime|Não aplicável|  
|timestamp|String|Caractere de 8 bits<sup>1</sup>|  
|TINYINT|Integer|Caractere de 8 bits<sup>1</sup>|  
|UDT|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|UNIQUEIDENTIFIER|String<sup>9</sup>|Caractere de 8 bits<sup>1</sup>|  
|varbinary|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|varbinary(MAX)|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|varchar|String|Caractere de 8 bits<sup>1</sup>|  
|varchar(MAX)|Fluxo<sup>2</sup>|Caractere de 8 bits<sup>1</sup>|
|Xml|Fluxo<sup>2</sup>|Caractere de 8 bits<sup>1</sup>|  
  

1.  Os dados são retornados em caracteres de 8 bits conforme especificado na página de código da localidade do Windows definida no sistema. Todos os caracteres multibyte ou caracteres não mapeados nessa página de código são substituídos por um caractere de ponto de interrogação (?) de byte único.  
  
2.  Se [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) ou [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) for usado para recuperar dados com o tipo PHP padrão de fluxo, os dados serão retornados como uma cadeia de caracteres com a mesma codificação que o fluxo. Por exemplo, se um tipo binário do SQL Server for recuperado usando **sqlsrv_fetch_array**, o tipo de retorno padrão será uma cadeia de caracteres binária.  
  
3.  Os dados são retornados do servidor como um fluxo de bytes brutos, sem codificação ou conversão.  

4.  Tipos de data e hora podem ser recuperados como cadeias de caracteres. Para obter mais informações, consulte [Como recuperar um tipo de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).  

5.  Esse é um tipo herdado que é mapeado para o tipo varbinary(max).

6. Esse é um tipo herdado que é mapeado para o tipo nvarchar(max).

7.  sql_variant não é compatível com parâmetros bidirecionais nem de saída.

8.  Esse é um tipo herdado que é mapeado para o tipo varchar(max).  
  
9.  UNIQUEIDENTIFIERs são GUIDs representados pela seguinte expressão regular:  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>Outros tipos de dados e recursos novos do SQL Server 2008  
Os tipos de dados novos do SQL Server 2008 e que existem fora das colunas (como parâmetros com valor de tabela) não são compatíveis com o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. A tabela a seguir resume o suporte do PHP para os novos recursos do SQL Server 2008.  
  
|Recurso|Suporte do PHP|  
|-----------|---------------|  
|Parâmetro com valor de tabela|Não|  
|Colunas esparsas|Parcial|  
|Compactação de bit nulo|Sim|  
|Tipos de dados CLR grande definidos pelo usuário (UDTs)|Sim|  
|Nome da entidade de serviço|Não|  
|MESCLAR|Sim|  
|FILESTREAM|Parcial|  
  
O suporte a tipo parcial significa que você não pode consultar programaticamente o tipo da coluna.  
  
## <a name="see-also"></a>Consulte Também  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)

[Convertendo tipos de dados](../../connect/php/converting-data-types.md)

[Tipos do PHP](https://php.net/manual/en/language.types.php)

[Tipos de dados (Transact-SQL)](../../t-sql/data-types/data-types-transact-sql.md)

[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  
