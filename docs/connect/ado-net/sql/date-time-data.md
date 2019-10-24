---
title: Dados de data e hora
description: Descreve como usar os novos tipos de dados de data e hora introduzidos no SQL Server 2008.
ms.date: 09/30/2019
dev_langs:
- csharp
ms.assetid: 6f5ff56a-a57e-49d7-8ae9-bbed697e42e3
ms.prod: sql
ms.prod_service: connectivity
ms.technology: connectivity
ms.topic: conceptual
author: v-kaywon
ms.author: v-kaywon
ms.reviewer: rothja
ms.openlocfilehash: 38626c6c726b9f45bd2d37d5deda480880556856
ms.sourcegitcommit: 9c993112842dfffe7176decd79a885dbb192a927
ms.translationtype: MTE75
ms.contentlocale: pt-BR
ms.lasthandoff: 10/16/2019
ms.locfileid: "72452254"
---
# <a name="date-and-time-data"></a>Dados de data e hora

![Download-DownArrow-Circled](../../../ssdt/media/download.png)[Download ADO.NET](../../sql-connection-libraries.md#anchor-20-drivers-relational-access)

SQL Server 2008 apresenta novos tipos de dados para o tratamento de informações de data e hora. Os novos tipos de dados incluem tipos separados para data e hora e tipos de dados expandidos com maior reconhecimento de intervalo, precisão e fuso horário. O Microsoft SqlClient Provedor de Dados for SQL Server (<xref:Microsoft.Data.SqlClient>) fornece suporte completo para todos os novos recursos do Mecanismo de Banco de Dados SQL Server 2008. Você deve instalar o .NET Framework 3,5 SP1 (ou posterior) ou o .NET Core 1,0 (ou posterior) para usar esses novos recursos com o SqlClient.  
  
As versões de SQL Server anteriores à SQL Server 2008 tinham apenas dois tipos de dados para trabalhar com valores de data e hora: `datetime` e `smalldatetime`. Ambos os tipos de dados contêm o valor de data e um valor de hora, o que dificulta o trabalho apenas com valores de data ou hora. Além disso, esses tipos de dados só dão suporte a datas que ocorrem após a introdução do calendário gregoriano na Inglaterra em 1753. Outra limitação é que esses tipos de dados mais antigos não têm reconhecimento de fuso horário, o que dificulta o trabalho com dados provenientes de vários fusos horários.  
  
A documentação completa para SQL Server tipos de dados está disponível em Manuais Online do SQL Server. Consulte [usando dados de data e hora](https://go.microsoft.com/fwlink/?LinkID=98361) para obter tópicos de nível de entrada sobre dados de data e hora.
  
## <a name="datetime-data-types-introduced-in-sql-server-2008"></a>Tipos de dados de Data/Hora introduzidos no SQL Server 2008  
 A tabela a seguir descreve os novos tipos de dados de data e hora.  
  
|Tipo de dados do SQL Server|Descrição|  
|--------------------------|-----------------|  
|`date`|O tipo de dados `date` tem um intervalo de 1º de janeiro de 01 a 31 de dezembro de 9999 com precisão de 1 dia. O valor padrão é 1 de janeiro de 1900. O tamanho do armazenamento é 3 bytes.|  
|`time`|O tipo de dados `time` armazena somente valores de tempo, com base em um relógio de 24 horas. O tipo de dados `time` tem um intervalo de 00:00:00.0000000 a 23:59:59.9999999 com precisão de 100 nanossegundos. O valor padrão é 00:00:00.0000000 (meia-noite). O tipo de dados `time` dá suporte à precisão de fração de segundo definida pelo usuário e o tamanho do armazenamento varia de 3 a 6 bytes, com base na precisão especificada.|  
|`datetime2`|O tipo de dados `datetime2` combina o intervalo e a precisão do `date` e `time` tipos de dados em um único tipo de dados.<br /><br /> Os valores padrão e os formatos literais de cadeia de caracteres são os mesmos definidos nos tipos de dados `date` e `time`.|  
|`datetimeoffset`|O tipo de dados `datetimeoffset` tem todos os recursos de `datetime2` com um deslocamento de fuso horário adicional. O deslocamento de fuso horário é representado como [+&#124;-] HH:MM. HH equivale a dois dígitos, variando de 00 a 14, que representam o número de horas no deslocamento de fuso horário. MM equivale a dois dígitos, variando de 00 a 59, que representam o número de minutos adicionais no deslocamento de fuso horário. Os formatos de hora têm suporte em 100 nanossegundos. O obrigatório + ou-Sign indica se o deslocamento de fuso horário é adicionado ou subtraído do UTC (coordenada universal de tempo ou hora de Greenwich) para obter a hora local.|  
  
> [!NOTE]
>  Para obter mais informações sobre o uso da palavra-chave `Type System Version`, confira <xref:Microsoft.Data.SqlClient.SqlConnection.ConnectionString%2A>.  
  
## <a name="date-format-and-date-order"></a>Formato de data e ordem de data  
Como SQL Server analisa os valores de data e hora depende não apenas da versão do sistema de tipos e da versão do servidor, mas também das configurações de formato e idioma padrão do servidor. Uma cadeia de caracteres de data que funciona para os formatos de data de um idioma pode ser irreconhecível se a consulta for executada por uma conexão que usa uma configuração de idioma e formato de data diferente.  
  
A instrução SET LANGUAGE do Transact-SQL define implicitamente o DATEFORMAT que determina a ordem das partes de data. Você pode usar a instrução SET DATEFORMAT Transact-SQL em uma conexão para desambiguar valores de data ordenando as partes de data em MDY, DMY, YMD, YDM, MYD ou DYM Order.  
  
Se você não especificar nenhum DATEFORMAT para a conexão, SQL Server usará o idioma padrão associado à conexão. Por exemplo, uma cadeia de caracteres de data de ' 01/02/03 ' seria interpretada como MDY (2 de janeiro de 2003) em um servidor com uma configuração de idioma de Estados Unidos Inglês e como DMY (1 de fevereiro de 2003) em um servidor com uma configuração de idioma de inglês britânico. O ano é determinado usando a regra de ano corte SQL Server, que define a data de corte para atribuir o valor do século. Para obter mais informações, confira [Opção de corte de ano de dois dígitos](https://go.microsoft.com/fwlink/?LinkId=120473) nos Manuais Online do SQL Server.  
  
> [!NOTE]
>  Não há suporte para o formato de data YDM ao converter de um formato de cadeia de caracteres em `date`, `time`, `datetime2` ou `datetimeoffset`.  
  
Para obter mais informações sobre como o SQL Server interpreta dados de data e hora, confira [Usando dados de data e hora](https://go.microsoft.com/fwlink/?LinkID=98361) nos Manuais Online do SQL Server 2008.  
  
## <a name="datetime-data-types-and-parameters"></a>Parâmetros e tipos de dados de data/hora  
As enumerações a seguir foram adicionadas ao <xref:System.Data.SqlDbType> para dar suporte aos novos tipos de dados de data e hora.  
  
- `SqlDbType.Date`  
  
- `SqlDbType.Time`  
  
- `SqlDbType.DateTime2`  
  
- `SqlDbType.DateTimeOffSet`  

Você pode especificar o tipo de dados de um <xref:Microsoft.Data.SqlClient.SqlParameter> usando uma das enumerações <xref:System.Data.SqlDbType> anteriores. 

> [!NOTE]
> Não é possível definir a propriedade `DbType` de um `SqlParameter` como `SqlDbType.Date`.

Você também pode especificar o tipo de um <xref:Microsoft.Data.SqlClient.SqlParameter> genericamente definindo a propriedade <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> de um objeto `SqlParameter` para um determinado valor de enumeração de <xref:System.Data.DbType>. Os seguintes valores de enumeração foram adicionados ao <xref:System.Data.DbType> para dar suporte aos tipos de dados `datetime2` e `datetimeoffset`:  
  
- DbType. DateTime2  
  
- DbType. DateTimeOffset  
  
Essas novas enumerações complementam as enumerações `Date`, `Time` e `DateTime`.  
  
O tipo de Provedor de Dados do Microsoft SqlClient de um objeto de parâmetro é inferido do tipo .NET do valor do objeto Parameter ou da `DbType` do objeto Parameter. Nenhum tipo de dados novo <xref:System.Data.SqlTypes> foi introduzido para dar suporte aos novos tipos de dados de data e hora. A tabela a seguir descreve os mapeamentos entre os tipos de dados de data e hora do SQL Server 2008 e os tipos de dados do CLR.  
  
|Tipo de dados do SQL Server|Tipo .NET|System. Data. SqlDbType|System. Data. DbType|  
|--------------------------|-------------------------|---------------------------|------------------------|  
|Data|System.DateTime|data|data|  
|time|System.TimeSpan|Hora|Hora|  
|datetime2|System.DateTime|datetime2|datetime2|  
|datetimeoffset|System.DateTimeOffset|DateTimeOffset|DateTimeOffset|  
|DATETIME|System.DateTime|DateTime|DateTime|  
|smalldatetime|System.DateTime|DateTime|DateTime|  
  
### <a name="sqlparameter-properties"></a>Propriedades do SqlParameter  
 A tabela a seguir descreve `SqlParameter` propriedades que são relevantes para os tipos de dados de data e hora.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.IsNullable%2A>|Obtém ou define se um valor é anulável. Ao enviar um valor de parâmetro nulo para o servidor, você deve especificar <xref:System.DBNull>, em vez de `null` (`Nothing` em Visual Basic). Para obter mais informações sobre nulos de banco de dados, consulte [lidando com valores nulos](handle-null-values.md).|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Precision%2A>|Obtém ou define o número máximo de dígitos usados para representar o valor. Essa configuração é ignorada para tipos de dados de data e hora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Scale%2A>|Obtém ou define o número de casas decimais para as quais a parte de hora do valor é resolvida para `Time`, `DateTime2` e `DateTimeOffset`. O valor padrão é 0, o que significa que a escala real é inferida a partir do valor e enviada ao servidor.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Size%2A>|Ignorado para tipos de dados de data e hora.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.Value%2A>|Obtém ou define o valor do parâmetro.|  
|<xref:Microsoft.Data.SqlClient.SqlParameter.SqlValue%2A>|Obtém ou define o valor do parâmetro.|  
  
> [!NOTE]
>  Valores de tempo menores que zero ou maiores ou iguais a 24 horas lançarão um <xref:System.ArgumentException>.  
  
### <a name="creating-parameters"></a>Criar parâmetros  
Você pode criar um objeto <xref:Microsoft.Data.SqlClient.SqlParameter> usando seu construtor ou adicionando-o a um <xref:Microsoft.Data.SqlClient.SqlCommand>. <xref:Microsoft.Data.SqlClient.SqlCommand.Parameters%2A> coleção chamando o método `Add` da <xref:Microsoft.Data.SqlClient.SqlParameterCollection>. O método `Add` usará como entrada argumentos de construtor ou um objeto de parâmetro existente.  
  
As próximas seções neste tópico fornecem exemplos de como especificar parâmetros de data e hora.
  
### <a name="date-example"></a>Exemplo de data  
O fragmento de código a seguir demonstra como especificar um parâmetro `date`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Date";  
parameter.SqlDbType = SqlDbType.Date;  
parameter.Value = "2007/12/1";  
```  
  
### <a name="time-example"></a>Exemplo de tempo  
O fragmento de código a seguir demonstra como especificar um parâmetro `time`.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@time";  
parameter.SqlDbType = SqlDbType.Time;  
parameter.Value = DateTime.Parse("23:59:59").TimeOfDay;  
```  
  
### <a name="datetime2-example"></a>Exemplo de Datetime2  
O fragmento de código a seguir demonstra como especificar um parâmetro de `datetime2` com as partes de data e hora.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@Datetime2";  
parameter.SqlDbType = SqlDbType.DateTime2;  
parameter.Value = DateTime.Parse("1666-09-02 1:00:00");  
```  
  
### <a name="datetimeoffset-example"></a>Exemplo de DateTimeOffSet  
O fragmento de código a seguir demonstra como especificar um parâmetro `DateTimeOffSet` com uma data, uma hora e um deslocamento de fuso horário de 0.  
  
```csharp  
SqlParameter parameter = new SqlParameter();  
parameter.ParameterName = "@DateTimeOffSet";  
parameter.SqlDbType = SqlDbType.DateTimeOffSet;  
parameter.Value = DateTimeOffset.Parse("1666-09-02 1:00:00+0");  
```  
  
### <a name="addwithvalue"></a>Addcomvalue  
Você também pode fornecer parâmetros usando o método `AddWithValue` de um <xref:Microsoft.Data.SqlClient.SqlCommand>, conforme mostrado no fragmento de código a seguir. No entanto, o método `AddWithValue` não permite que você especifique o <xref:Microsoft.Data.SqlClient.SqlParameter.DbType%2A> ou <xref:Microsoft.Data.SqlClient.SqlParameter.SqlDbType%2A> para o parâmetro.  
  
```csharp  
command.Parameters.AddWithValue(   
    "@date", DateTimeOffset.Parse("16660902"));  
```  
  
O parâmetro `@date` pode mapear para um tipo de dados `date`, `datetime` ou `datetime2` no servidor. Ao trabalhar com os novos tipos de dados `datetime`, você deve definir explicitamente a propriedade <xref:System.Data.SqlDbType> do parâmetro como o tipo de dados da instância. Usar <xref:System.Data.SqlDbType.Variant> ou fornecer valores de parâmetro implicitamente pode causar problemas com a compatibilidade com versões anteriores com os tipos de dados `datetime` e `smalldatetime`.  
  
A tabela a seguir mostra quais `SqlDbTypes` são inferidas a partir dos tipos CLR:  
  
|Tipo CLR|SqlDbType inferido|  
|--------------|------------------------|  
|DateTime|SqlDbType. DateTime|  
|TimeSpan|SqlDbType. time|  
|DateTimeOffset|SqlDbType. DateTimeOffset|  
  
## <a name="retrieving-date-and-time-data"></a>Recuperando dados de data e hora  
A tabela a seguir descreve os métodos que são usados para recuperar SQL Server valores de data e hora do 2008.  
  
|Método SqlClient|Descrição|  
|----------------------|-----------------|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTime%2A>|Recupera o valor da coluna especificada como uma estrutura de <xref:System.DateTime>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetDateTimeOffset%2A>|Recupera o valor da coluna especificada como uma estrutura de <xref:System.DateTimeOffset>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificFieldType%2A>|Retorna o tipo que é o tipo específico do provedor subjacente para o campo. Retorna os mesmos tipos que `GetFieldType` para novos tipos de data e hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValue%2A>|Recupera o valor da coluna especificada. Retorna os mesmos tipos que `GetValue` para os novos tipos de data e hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetProviderSpecificValues%2A>|Recupera os valores na matriz especificada.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlString%2A>|Recupera o valor da coluna como um <xref:System.Data.SqlTypes.SqlString>. Um <xref:System.InvalidCastException> ocorre se os dados não puderem ser expressos como um `SqlString`.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValue%2A>|Recupera os dados da coluna como seu `SqlDbType` padrão. Retorna os mesmos tipos que `GetValue` para os novos tipos de data e hora.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSqlValues%2A>|Recupera os valores na matriz especificada.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetString%2A>|Recupera o valor da coluna como uma cadeia de caracteres se a versão do sistema do tipo estiver definida como SQL Server 2005. Um <xref:System.InvalidCastException> ocorre se os dados não puderem ser expressos como uma cadeia de caracteres.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetTimeSpan%2A>|Recupera o valor da coluna especificada como uma estrutura de <xref:System.TimeSpan>.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValue%2A>|Recupera o valor da coluna especificada como seu tipo CLR subjacente.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetValues%2A>|Recupera valores de coluna em uma matriz.|  
|<xref:Microsoft.Data.SqlClient.SqlDataReader.GetSchemaTable%2A>|Retorna um <xref:System.Data.DataTable> que descreve os metadados do conjunto de resultados.|  
  
> [!NOTE]
>  Não há suporte para a nova `SqlDbTypes` de data e hora para o código que está executando em processo no SQL Server. Uma exceção será gerada se um desses tipos for passado para o servidor.  
  
## <a name="specifying-date-and-time-values-as-literals"></a>Especificando valores de data e hora como literais  
Você pode especificar tipos de dados de data e hora usando uma variedade de formatos de cadeia de caracteres literais diferentes, que SQL Server avalia em tempo de execução, convertendo-os em estruturas de data/hora internas. SQL Server reconhece dados de data e hora que estão entre aspas simples ('). Os exemplos a seguir demonstram alguns formatos:  
  
- Formatos de datas alfabéticos, como `'October 15, 2006'`.  
  
- Formatos de data numéricos, como `'10/15/2006'`.  
  
- Formatos de cadeia de caracteres não separados, como `'20061015'`, que seriam interpretados como 15 de outubro de 2006 se você estiver usando o formato de data padrão ISO.  
  
> [!NOTE]
>  Você pode encontrar a documentação completa para todos os formatos de cadeia de caracteres literais e outros recursos dos tipos de dados de data e hora no Manuais Online do SQL Server.  
  
Valores de tempo menores que zero ou maiores ou iguais a 24 horas lançarão um <xref:System.ArgumentException>.  
  
## <a name="resources-in-sql-server-2008-books-online"></a>Recursos nos manuais online do SQL Server 2008  
Para obter mais informações sobre como trabalhar com valores de data e hora no SQL Server 2008, consulte os seguintes recursos nos manuais online do SQL Server 2008.  
  
|Tópico|Descrição|  
|-----------|-----------------|  
|[tipos de dados e funções de data e hora (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98360)|Fornece uma visão geral de todos os tipos de dados e as funções de data e hora do Transact-SQL.|  
|[Usando dados de data e hora](https://go.microsoft.com/fwlink/?LinkId=98361)|Fornece informações sobre os tipos de dados e funções de data e hora e exemplos de como usá-los.|  
|[Tipos de dados (Transact-SQL)](https://go.microsoft.com/fwlink/?LinkId=98362)|Descreve os tipos de dados do sistema no SQL Server 2008.|  
  
## <a name="next-steps"></a>Próximas etapas
- [Tipos de dados do SQL Server e do ADO.NET](sql-server-data-types.md)
