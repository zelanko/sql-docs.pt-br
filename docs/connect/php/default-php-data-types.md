---
title: Default PHP Data Types | Microsoft Docs
ms.custom: 
ms.date: 01/19/2017
ms.prod: sql-non-specified
ms.reviewer: 
ms.suite: 
ms.technology:
- drivers
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- default data types
- converting data types
ms.assetid: b66c301d-3d20-45b8-a112-225d8f01c0bd
caps.latest.revision: 40
author: MightyPen
ms.author: genemi
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: f7e6274d77a9cdd4de6cbcaef559ca99f77b3608
ms.openlocfilehash: 2db2186adfe8fc12a80c1459a0e5b768dfd9fe45
ms.contentlocale: pt-br
ms.lasthandoff: 09/09/2017

---
# <a name="default-php-data-types"></a>Tipos de dados padrão do PHP
[!INCLUDE[Driver_PHP_Download](../../includes/driver_php_download.md)]

Ao recuperar dados do servidor, o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)] converte os dados em um tipo de dados padrão do PHP se nenhum tipo de dados do PHP foi especificado pelo usuário.  
  
Quando dados são retornados usando o driver PDO_SQLSRV, o tipo de dados é int ou cadeia de caracteres.  
  
O restante deste tópico aborda os tipos de dados padrão usando o driver SQLSRV.  
  
A tabela a seguir lista o tipo de dados do SQL Server (o tipo de dados que está sendo recuperado do servidor), o tipo de dados padrão do PHP (o tipo de dados no qual os dados são convertidos) e a codificação padrão para fluxos e cadeias de caracteres. Para obter detalhes sobre como especificar tipos de dados ao recuperar dados do servidor, consulte [How to: Specify PHP Data Types](../../connect/php/how-to-specify-php-data-types.md).  
  
|Tipo do SQL Server|Tipo padrão do PHP|Codificação padrão|  
|-------------------|--------------------|--------------------|  
|bigint|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|binary|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|bit|Integer|caracteres de 8 bits<sup>1</sup>|  
|char|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|date<sup>4</sup>|Datetime|Não aplicável|  
|DateTime<sup>4</sup>|Datetime|Não aplicável|  
|datetime2<sup>4</sup>|Datetime|Não aplicável|  
|datetimeoffset<sup>4</sup>|Datetime|Não aplicável|  
|decimal|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|float|Valor Flutuante|caracteres de 8 bits<sup>1</sup>|  
|geografia|Fluxo|Binário<sup>3</sup>|  
|geometria|Fluxo|Binário<sup>3</sup>|  
|imagem<sup>5</sup>|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|int|Integer|caracteres de 8 bits<sup>1</sup>|  
|money|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|nchar|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|numeric|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|nvarchar|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|nvarchar(MAX)|Fluxo<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|ntext<sup>6</sup>|Fluxo<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|real|Valor Flutuante|caracteres de 8 bits<sup>1</sup>|  
|smalldatetime|Datetime|caracteres de 8 bits<sup>1</sup>|  
|smallint|Integer|caracteres de 8 bits<sup>1</sup>|  
|smallmoney|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|sql_variant<sup>7</sup>|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|texto<sup>8</sup>|Fluxo<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
|time<sup>4</sup>|Datetime|Não aplicável|  
|timestamp|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|tinyint|Integer|caracteres de 8 bits<sup>1</sup>|  
|UDT|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|uniqueidentifier|Cadeia de caracteres<sup>9</sup>|caracteres de 8 bits<sup>1</sup>|  
|varbinary|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|varbinary(MAX)|Fluxo<sup>2</sup>|Binário<sup>3</sup>|  
|varchar|Cadeia de caracteres|caracteres de 8 bits<sup>1</sup>|  
|varchar(MAX)|Fluxo<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|
|xml|Fluxo<sup>2</sup>|caracteres de 8 bits<sup>1</sup>|  
  

1.  Dados são retornados em caracteres de 8 bits conforme especificado na página de código da localidade do Windows definida no sistema. Todos os caracteres multibyte ou caracteres não mapeados nessa página de código são substituídos por um caractere de ponto de interrogação (?) de byte único.  
  
2.  Se [sqlsrv_fetch_array](../../connect/php/sqlsrv-fetch-array.md) ou [sqlsrv_fetch_object](../../connect/php/sqlsrv-fetch-object.md) for usado para recuperar dados com o tipo PHP padrão de fluxo, os dados serão retornados como uma cadeia de caracteres com a mesma codificação que o fluxo. Por exemplo, se um tipo binário do SQL Server for recuperado usando **sqlsrv_fetch_array**, o tipo de retorno padrão será uma cadeia de caracteres binária.  
  
3.  Os dados são retornados do servidor como um fluxo de bytes brutos, sem codificação ou conversão.  

4.  Tipos de data e hora podem ser recuperados como cadeias de caracteres. Para obter mais informações, consulte [Como recuperar um tipo de data e hora como cadeias de caracteres usando o driver SQLSRV](../../connect/php/how-to-retrieve-date-and-time-type-as-strings-using-the-sqlsrv-driver.md).  

5.  Esse é um tipo herdado que é mapeado para o tipo varbinary(max).

6. Esse é um tipo herdado que é mapeado para o tipo nvarchar(max).

7.  Não há suporte para sql_variant parâmetros bidirecional ou de saída.

8.  Esse é um tipo herdado que é mapeado para o tipo varchar(max).  
  
9.  UNIQUEIDENTIFIERs são GUIDs representados pela seguinte expressão regular:  
  
    [0-9a-fA-F]{8}-[0-9a-fA-F]{4}-[0-9a-fA-f]{4}-[0-9a-fA-f]{4}-[0-9a-fA-F]{12}  
 
 
## <a name="other-new-sql-server-2008-data-types-and-features"></a>Outros tipos de dados e recursos novos do SQL Server 2008  
Tipos de dados que são novos no SQL Server 2008 e que existem fora das colunas (como parâmetros com valor de tabela) não há suporte para o [!INCLUDE[ssDriverPHP](../../includes/ssdriverphp_md.md)]. A tabela a seguir resume o suporte do PHP para os novos recursos do SQL Server 2008.  
  
|Recurso|Suporte do PHP|  
|-----------|---------------|  
|Parâmetro com valor de tabela|Não|  
|Colunas esparsas|Parcial|  
|Compactação de bit nulo|Sim|  
|Tipos de dados CLR grande definidos pelo usuário (UDTs)|Sim|  
|Nome da entidade de serviço|Não|  
|MERGE|Sim|  
|FILESTREAM|Parcial|  
  
O suporte a tipo parcial significa que você não pode consultar programaticamente o tipo da coluna.  
  
## <a name="see-also"></a>Consulte também  
[Constantes &#40;Drivers da Microsoft para PHP para SQL Server&#41;](../../connect/php/constants-microsoft-drivers-for-php-for-sql-server.md)  
[Converting Data Types](../../connect/php/converting-data-types.md)  
[Tipos do PHP](http://go.microsoft.com/fwlink/?LinkId=109071)  
[Tipos de dados (Transact-SQL)](http://go.microsoft.com/fwlink/?LinkId=109068)  
[sqlsrv_field_metadata](../../connect/php/sqlsrv-field-metadata.md)  
  

