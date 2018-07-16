---
title: Parâmetros e códigos de retorno na tarefa Executar SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- return codes [Integration Services]
- parameters [Integration Services]
- parameterized SQL statements [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: a3ca65e8-65cf-4272-9a81-765a706b8663
caps.latest.revision: 28
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 12739be23eb0a2104f73d9ad1c1240b3c235259c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37252328"
---
# <a name="parameters-and-return-codes-in-the-execute-sql-task"></a>Parâmetros e códigos de retorno na Tarefa Executar SQL
  Instruções SQL e procedimentos armazenados frequentemente usam `input` parâmetros, `output` parâmetros e códigos de retorno. No [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], a tarefa Executar SQL tem suporte para os tipos de parâmetros `Input`, `Output` e `ReturnValue`. Você usa o `Input` tipo para parâmetros de entrada `Output` para parâmetros de saída e `ReturnValue` para códigos de retorno.  
  
> [!NOTE]  
>  Você só poderá usar parâmetros em uma tarefa Executar SQL se o provedor de dados der suporte a eles.  
  
 Os parâmetros em comandos SQL, inclusive consultas e procedimentos armazenados, são mapeados para variáveis definidas pelo usuário criadas no escopo da tarefa Executar SQL, um contêiner pai ou no escopo do pacote. Os valores das variáveis podem ser definidos em tempo de projeto ou populados dinamicamente em tempo de execução. Você também pode mapear parâmetros para variáveis de sistema. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](integration-services-ssis-variables.md) e [Variáveis do Sistema](system-variables.md).  
  
 No entanto, trabalhar com parâmetros e códigos de retorno em uma tarefa Executar SQL é mais do que apenas saber para quais tipos de parâmetro a tarefa tem suporte e como esses parâmetros serão mapeados. Há requisitos de uso adicionais e diretrizes para usar parâmetros e códigos de retorno de modo bem-sucedido na tarefa Executar SQL. Esses requisitos de uso e diretrizes são abordados no restante deste tópico:  
  
-   [Usando nomes e marcadores de parâmetros](#Parameter_names_and_markers)  
  
-   [Usando parâmetros com tipos de dados de data e hora](#Date_and_time_data_types)  
  
-   [Usando parâmetros em cláusulas WHERE](#WHERE_clauses)  
  
-   [Usando parâmetros com procedimentos armazenados](#Stored_procedures)  
  
-   [Obtendo valores de códigos de retorno](#Return_codes)  
  
-   [Configurando parâmetros e códigos de retorno no Execute SQL Editor da tarefa](#Configure_parameters_and_return_codes)  
  
##  <a name="Parameter_names_and_markers"></a> Usar marcadores e nomes de parâmetro  
 Dependendo do tipo de conexão usado pela tarefa Executar SQL, a sintaxe do comando SQL utiliza marcadores de parâmetro diferentes. Por exemplo, o tipo de gerenciador de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] exige que o comando SQL use um marcador de parâmetro no formato **@varParameter**, enquanto que o tipo de conexão OLE DB exige o marcador de parâmetro ponto de interrogação (?).  
  
 Os nomes que você pode usar como nomes de parâmetro nos mapeamentos entre as variáveis e os parâmetros também variam por tipo de gerenciador de conexões. Por exemplo, o tipo de gerenciador de conexão [!INCLUDE[vstecado](../includes/vstecado-md.md)] usa um nome definido pelo usuário com um prefixo @, enquanto o tipo de gerenciador de conexões OLE DB requer que você use o valor numérico de ordinal de base 0 como o nome do parâmetro.  
  
 A tabela a seguir resume os requisitos de comandos SQL para os tipos de gerenciador de conexões que podem ser utilizados pela tarefa Executar SQL.  
  
|Tipo de conexão|Marcador de parâmetro|Nome do parâmetro|Exemplo de comando SQL|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2,...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|@\<nome do parâmetro>|@\<nome do parâmetro>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = @parmContactID|  
|ODBC|?|1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL e OLE DB|?|0, 1, 2, 3, …|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
### <a name="using-parameters-with-adonet-and-ado-connection-managers"></a>Usando parâmetros com os gerenciadores de conexões ADO.NET e ADO  
 Gerenciadores de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] e ADO têm requisitos específicos para comandos SQL que usam parâmetros:  
  
-   Gerenciadores de conexões [!INCLUDE[vstecado](../includes/vstecado-md.md)] requerem que o comando SQL use nomes de parâmetro como marcadores de parâmetro. Isso significa que as variáveis podem ser mapeadas diretamente para parâmetros. Por exemplo, a variável `@varName` é mapeada para o parâmetro denominado `@parName` e fornece um valor para o parâmetro `@parName`.  
  
-   Os gerenciadores de conexões ADO requerem que o comando SQL use pontos de interrogação (?) como marcadores de parâmetro. No entanto, você pode usar qualquer nome definido pelo usuário, com exceção de valores de número inteiro, como nomes de parâmetro.  
  
 Para fornecer valores a parâmetros, as variáveis são mapeadas para nomes de parâmetro. Em seguida, a tarefa Executar SQL usa o valor ordinal do nome do parâmetro na lista de parâmetros para carregar valores de variáveis a parâmetros.  
  
### <a name="using-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Usando parâmetros com os gerenciadores de conexões EXCEL, ODBC e OLE DB  
 Os gerenciadores de conexões EXCEL, ODBC e OLE DB requerem que o comando SQL use pontos de interrogação (?) como marcadores de parâmetro e valores numéricos de base 0 ou base 1 como nomes de parâmetros. Se a tarefa Executar SQL utilizar o gerenciador de conexões ODBC, o nome do parâmetro mapeado para o primeiro parâmetro na consulta será denominado 1; caso contrário, o parâmetro será denominado 0. Para os parâmetros subsequentes, o valor numérico do nome do parâmetro indica o parâmetro no comando SQL para o qual o nome do parâmetro é mapeado. Por exemplo, o parâmetro denominado 3 é mapeado para o terceiro parâmetro, que é representado pelo terceiro ponto de interrogação (?) no comando SQL.  
  
 Para fornecer valores a parâmetros, as variáveis são mapeadas para nomes de parâmetros e a tarefa Executar SQL usa o valor ordinal do nome do parâmetro para carregar valores de variáveis a parâmetros.  
  
 Dependendo do provedor utilizado pelo gerenciador de conexões, alguns tipos de dados OLE DB talvez não tenham suporte. Por exemplo, o driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Para obter mais informações sobre o comportamento do provedor Jet com o driver do Excel, consulte [Origem do Excel](data-flow/excel-source.md).  
  
#### <a name="using-parameters-with-ole-db-connection-managers"></a>Usando parâmetros com gerenciadores de conexões OLE DB  
 Quando a tarefa Executar SQL usa o gerenciador de conexões OLE DB, a propriedade BypassPrepare da tarefa está disponível. Você deve definir essa propriedade `true` se a tarefa Executar SQL usar instruções SQL com parâmetros.  
  
 Quando você usa um gerenciador de conexões OLE DB, não pode usar subconsultas com parâmetros, porque a tarefa Executar SQL não pode derivar informações de parâmetro por meio do provedor OLE DB. Entretanto, você pode usar uma expressão para concatenar os valores de parâmetro na cadeia de caracteres de consulta de definir a propriedade SqlStatementSource da tarefa.  
  
##  <a name="Date_and_time_data_types"></a> Usando parâmetros com tipos de dados de hora e data  
  
### <a name="using-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Usando parâmetros de data e hora com os gerenciadores de conexões ADO.NET e ADO  
 Ao ler dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tipos `time` e `datetimeoffset`, uma tarefa Executar SQL que usa um [!INCLUDE[vstecado](../includes/vstecado-md.md)] ou Gerenciador de conexão ADO tem os seguintes requisitos adicionais:  
  
-   Para `time` dados, uma [!INCLUDE[vstecado](../includes/vstecado-md.md)] Gerenciador de conexão requer que esses dados sejam armazenados em um parâmetro cujo tipo é `Input` ou `Output`, e cujo tipo de dados é `string`.  
  
-   Para `datetimeoffset` dados, um [!INCLUDE[vstecado](../includes/vstecado-md.md)] Gerenciador de conexão requer que esses dados sejam armazenados em um dos seguintes parâmetros:  
  
    -   Um parâmetro cujo tipo é `Input` e cujo tipo de dados é `string`.  
  
    -   Um parâmetro cujo tipo é `Output` ou `ReturnValue`, e cujo tipo de dados é `datetimeoffset`, `string`, ou `datetime2`. Se você selecionar um parâmetro cujo tipo de dados é `string` ou `datetime2`, [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] converte os dados em string ou datetime2.  
  
-   Um gerenciador de conexões ADO requer que os dados `time` ou `datetimeoffset` sejam armazenados em um parâmetro cujo tipo é `Input` ou `Output` e cujo tipo de dados é `adVarWchar`.  
  
 Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](/sql/t-sql/data-types/data-types-transact-sql) e [Tipos de dados do Integration Services](data-flow/integration-services-data-types.md).  
  
### <a name="using-date-and-time-parameters-with-ole-db-connection-managers"></a>Usando parâmetros de data e hora com os gerenciadores de conexões OLE DB  
 Ao usar um Gerenciador de conexão OLE DB, uma tarefa Executar SQL tem requisitos específicos de armazenamento para dados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tipos de dados `date`, `time`, `datetime`, `datetime2`, e `datetimeoffset`. Você deve armazenar estes dados em um dos tipos de parâmetros seguintes:  
  
-   Um parâmetro de entrada do tipo de dados NVARCHAR.  
  
-   Um parâmetro de saída com o tipo de dados apropriado, como listado na tabela a seguir.  
  
    |Tipo de parâmetro `Output`|Tipo de dados de data|  
    |-------------------------------|--------------------|  
    |DBDATE|`date`|  
    |DBTIME2|`time`|  
    |DBTIMESTAMP|`datetime`, `datetime2`|  
    |DBTIMESTAMPOFFSET|`datetimeoffset`|  
  
 Se os dados não forem armazenados no parâmetro de entrada ou saída apropriado, o pacote falhará.  
  
### <a name="using-date-and-time-parameters-with-odbc-connection-managers"></a>Usando parâmetros de data e hora com gerenciadores de conexões ODBC  
 Ao usar um Gerenciador de conexão ODBC, uma tarefa Executar SQL tem requisitos específicos de armazenamento para dados com um dos [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] tipos de dados `date`, `time`, `datetime`, `datetime2`, ou `datetimeoffset`. Você deve armazenar estes dados em um dos tipos de parâmetros seguintes:  
  
-   Um parâmetro `input` do tipo de dados SQL_WVARCHAR  
  
-   Um `output` parâmetro com o tipo de dados apropriado, conforme listado na tabela a seguir.  
  
    |Tipo de parâmetro `Output`|Tipo de dados de data|  
    |-------------------------------|--------------------|  
    |SQL_DATE|`date`|  
    |SQL_SS_TIME2|`time`|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -ou-<br /><br /> SQL_TIMESTAMP|`datetime`, `datetime2`|  
    |SQL_SS_TIMESTAMPOFFSET|`datetimeoffset`|  
  
 Se os dados não forem armazenados no parâmetro de entrada ou saída apropriado, o pacote falhará.  
  
##  <a name="WHERE_clauses"></a> Usando parâmetros em onde cláusulas  
 Os comandos SELECT, INSERT, UPDATE e DELETE frequentemente incluem cláusulas WHERE para especificar filtros que definem as condições que cada linha nas tabelas de origem devem atender para se qualificar para um comando SQL. Os parâmetros fornecem os valores de filtro nas cláusulas WHERE.  
  
 Você pode usar marcadores de parâmetro para fornecer valores de parâmetros dinamicamente. As regras para quais marcadores e nomes de parâmetros podem ser usados na instrução SQL dependem do tipo de gerenciador de conexões utilizado por Executar SQL.  
  
 A tabela a seguir lista exemplos do comando SELECT por tipo de gerenciador de conexões. As instruções INSERT, UPDATE e DELETE são semelhantes. Os exemplos usam SELECT para retornar produtos da tabela **Produto** em [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)] que tenham uma **ProductID** maior e menor que os valores especificados pelos dois parâmetros.  
  
|Tipo de conexão|Sintaxe de SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Os exemplos exigiriam parâmetros que têm os seguintes nomes:  
  
-   Os gerenciadores de conexões EXCEL e OLED DB usam os nomes de parâmetro 0 e 1. O tipo de conexão ODBC usa 1 e 2.  
  
-   O tipo de conexão ADO pode usar quaisquer dois nomes de parâmetro, como Param1 e Param2, mas os parâmetros devem ser mapeados pela posição original na lista de parâmetros.  
  
-   O tipo de conexão [!INCLUDE[vstecado](../includes/vstecado-md.md)] usa os nomes de parâmetro @parmMinProductID e @parmMaxProductID.  
  
##  <a name="Stored_procedures"></a> Usando parâmetros com procedimentos armazenados  
 Os comandos SQL que executam procedimentos armazenados também podem usar mapeamento de parâmetro. As regras de como usar marcadores e nomes de parâmetros dependem do tipo de gerenciador de conexões utilizado por Executar SQL, assim como as regras para consultas parametrizadas.  
  
 A tabela a seguir lista exemplos do comando EXEC por tipo de gerenciador de conexões. Os exemplos executam o procedimento armazenado **uspGetBillOfMaterials** em [!INCLUDE[ssSampleDBUserInputNonLocal](../includes/sssampledbuserinputnonlocal-md.md)]. O procedimento armazenado usa o `@StartProductID` e `@CheckDate` `input` parâmetros.  
  
|Tipo de conexão|Sintaxe de EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Para obter mais informações sobre a sintaxe de chamada ODBC, consulte o tópico [Procedure Parameters](http://go.microsoft.com/fwlink/?LinkId=89462)(Parâmetros de procedimento) na Referência do programador de ODBC na Biblioteca MSDN.|  
|ADO|Se IsQueryStoredProcedure for definido como `False`, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Se IsQueryStoredProcedure for definido como `True`, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Se IsQueryStoredProcedure for definido como `False`, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Se IsQueryStoredProcedure for definido como `True`, `uspGetBillOfMaterials`|  
  
 Para usar parâmetros de saída, a sintaxe requer que a palavra-chave OUTPUT seja colocada após cada marcador de parâmetro. Por exemplo, a sintaxe do parâmetro de saída a seguir está correta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Para obter mais informações sobre como usar parâmetros de entrada e saída com procedimentos armazenados Transact-SQL, consulte [EXECUTE &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/execute-transact-sql).  
  
##  <a name="Return_codes"></a> Obtendo valores de códigos de retorno  
 Um procedimento armazenado pode retornar um valor inteiro chamado código de retorno para indicar o status de execução de um procedimento. Para implementar códigos de retorno na tarefa Executar SQL, você pode usar parâmetros da `ReturnValue` tipo.  
  
 A tabela a seguir lista, por tipo de conexão, alguns exemplos de comandos EXEC que implementam códigos de retorno. Todos os exemplos usam um parâmetro `input`. As regras para como usar marcadores e nomes de parâmetro são os mesmos para todos os tipos de parâmetro —`Input`, `Output`, e `ReturnValue`.  
  
 Algumas sintaxes não dão suporte a literais de parâmetro. Nesse caso, você deve fornecer o valor dó parâmetro usando uma variável.  
  
|Tipo de conexão|Sintaxe de EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Para obter mais informações sobre a sintaxe de chamada ODBC, consulte o tópico [Procedure Parameters](http://go.microsoft.com/fwlink/?LinkId=89462)(Parâmetros de procedimento) na Referência do programador de ODBC na Biblioteca MSDN.|  
|ADO|Se IsQueryStoreProcedure for definido como `False`, `EXEC ? = myStoredProcedure 1`<br /><br /> Se IsQueryStoreProcedure for definido como `True`, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../includes/vstecado-md.md)]|Se IsQueryStoreProcedure for definido como `True`.<br /><br /> `myStoredProcedure`|  
  
 Na sintaxe mostrada na tabela anterior, a tarefa Executar SQL usa o tipo de fonte **Entrada Direta** para executar o procedimento armazenado. A tarefa Executar SQL também pode usar o tipo de fonte **Conexão de Arquivo** para executar um procedimento armazenado. Independentemente se a tarefa Executar SQL usa o **entrada direta** ou **arquivo de Conexão** tipo de fonte, use um parâmetro do `ReturnValue` tipo para implementar o código de retorno. Para obter mais informações sobre como configurar o tipo de fonte da instrução SQL executado pela tarefa Executar SQL, consulte [Editor da Tarefa Executar SQL &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md).  
  
 Para obter mais informações sobre como usar códigos de retorno com procedimentos armazenados Transact-SQL, consulte [RETURN &#40;Transact-SQL&#41;](/sql/t-sql/language-elements/return-transact-sql).  
  
##  <a name="Configure_parameters_and_return_codes"></a> Configurando parâmetros e códigos de retorno na tarefa Executar SQL  
 Para obter mais informações sobre as propriedades de parâmetros e códigos de retorno que podem ser definidas no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)], clique no seguinte tópico:  
  
-   [SQL Editor da tarefa executar &#40;página de mapeamento de parâmetro&#41;](../../2014/integration-services/execute-sql-task-editor-parameter-mapping-page.md)  
  
 Para obter mais informações sobre como definir essas propriedades no [!INCLUDE[ssIS](../includes/ssis-md.md)] Designer, clique no tópico a seguir:  
  
-   [Definir as propriedades de uma tarefa ou contêiner](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-tasks"></a>Related Tasks  
 [Definir as propriedades de uma tarefa ou contêiner](../../2014/integration-services/set-the-properties-of-a-task-or-container.md)  
  
## <a name="related-content"></a>Conteúdo relacionado  
  
-   Entrada de blog, [Stored procedures with output parameters](http://go.microsoft.com/fwlink/?LinkId=157786)(Procedimentos armazenados com parâmetros de saída) em blogs.msdn.com  
  
-   Exemplo do CodePlex, [Execute SQL Parameters and Result Sets (em inglês)](http://go.microsoft.com/fwlink/?LinkId=157863), em msftisprodsamples.codeplex.com  
  
## <a name="see-also"></a>Consulte também  
 [Tarefa Executar SQL](control-flow/execute-sql-task.md)   
 [Conjuntos de resultados na tarefa Executar SQL](../../2014/integration-services/result-sets-in-the-execute-sql-task.md)  
  
  
