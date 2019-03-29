---
title: Tarefa Executar SQL | Microsoft Docs
ms.custom: ''
ms.date: 03/13/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.executesqltask.f1
- sql13.dts.designer.executesqltask.general.f1
- sql13.dts.designer.executesqltask.parametermapping.f1
- sql13.dts.designer.executesqltask.resultset.f1
helpviewer_keywords:
- Transact-SQL statements, SSIS
- statements [Integration Services]
- batches [Integration Services]
- Execute SQL task [Integration Services]
ms.assetid: bebb2e8c-0410-43b2-ac2f-6fc80c8f2e9e
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: ff217e16fb9d153872d00074ff2f5d672be056d0
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58273910"
---
# <a name="execute-sql-task"></a>Tarefa Executar SQL
  A tarefa Executar SQL executa instruções SQL ou procedimentos armazenados a partir de um pacote. A tarefa pode conter uma única instrução SQL ou várias instruções SQL que são executadas em sequência. Você pode usar a tarefa Executar SQL para os seguintes propósitos:  
  
-   Truncar uma tabela ou exibição em preparação para inserção de dados.  
  
-   Criar, alterar e descartar objetos de banco de dados como tabelas e exibições.  
  
-   Recriar tabelas de fatos e de dimensões antes de carregar dados nelas.  
  
-   Executar procedimentos armazenados. Se a instrução SQL invocar um procedimento armazenado que retorne resultados de uma tabela temporária, use a opção de WITH RESULT SETS para definir metadados para o conjunto de resultados.  
  
-   Salvar o conjunto de linhas retornado de uma consulta em uma variável.  
  
 A tarefa Executar SQL pode ser usada em combinação com os contêineres Loop Foreach e Loop For para executar várias instruções SQL. Esses contêineres implementam fluxos de controle repetitivos em um pacote e eles podem executar a tarefa Executar SQL várias vezes. Por exemplo, usando o contêiner Loop Foreach, um pacote pode enumerar arquivos em uma pasta e executar uma tarefa Executar SQL várias vezes para executar a instrução SQL armazenada em cada arquivo.  
  
## <a name="connect-to-a-data-source"></a>Conectar-se a uma fonte de dados  
 A tarefa Executar SQL pode usar tipos diferentes de gerenciadores de conexões para se conectar à fonte de dados onde a instrução SQL ou o procedimento armazenado é executado. A tarefa pode usar os tipos de conexão listados na tabela a seguir.  
  
|Tipo de conexão|Gerenciador de conexões|  
|---------------------|------------------------|  
|EXCEL|[Gerenciador de Conexões do Excel](../../integration-services/connection-manager/excel-connection-manager.md)|  
|OLE DB|[Gerenciador de conexões OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)|  
|ODBC|[Gerenciador de Conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)|  
|ADO|[Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)|  
|ADO.NET|[Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)|  
|SQLMOBILE|[Gerenciador de Conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)|  
  
## <a name="create-sql-statements"></a>Criar instruções SQL  
 A origem das instruções SQL usada por essa tarefa pode ser uma propriedade de tarefa que contém uma instrução, uma conexão com um arquivo que contém uma ou várias instruções ou o nome de uma variável que contém uma instrução. As instruções SQL devem ser gravadas na linguagem do sistema de gerenciamento de banco de dados de origem (DBMS). Para obter mais informações, consulte [Consultas do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-queries.md).  
  
 Se as instruções SQL estiverem armazenadas em um arquivo, a tarefa usará um gerenciador de conexões de arquivo para se conectar ao arquivo. Para obter mais informações, consulte [File Connection Manager](../../integration-services/connection-manager/file-connection-manager.md).  
  
 No Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] , você pode usar a caixa de diálogo **Editor da Tarefa Executar SQL** para digitar instruções SQL ou usar o **Construtor de Consultas**, uma interface do usuário gráfica para criar consultas SQL. 
  
> [!NOTE]  
>  Instruções SQL válidas gravadas fora da tarefa Executar SQL talvez não sejam analisadas com êxito pela tarefa Executar SQL.  
  
> [!NOTE]  
>  A Tarefa Executar SQL usa o valor de enumeração **RecognizeAll** ParseMode. Para obter mais informações, consulte [Namespace ManagedBatchParser](https://go.microsoft.com/fwlink/?LinkId=223617).  
  
## <a name="send-multiple-statements-in-a-batch"></a>Enviar várias instruções em um lote  
 Se várias instruções forem incluídas em uma tarefa Executar SQL, é possível agrupá-las e executá-las como um lote. Para sinalizar o final de um lote, use o comando GO. Todas as instruções SQL entre dois comandos GO são enviadas em um lote para o provedor OLE DB a fim de serem executadas. O comando SQL pode incluir vários lotes separados por comandos GO.  
  
 Há restrições sobre os tipos de instruções SQL que podem ser agrupados em um lote. Para obter mais informações, consulte as instruções [Lotes de instruções](../../relational-databases/native-client-odbc-queries/executing-statements/batches-of-statements.md).  
  
 Se a tarefa Executar SQL executar um lote de instruções SQL, as seguintes regras se aplicam ao lote:  
  
-   Só uma instrução pode retornar um conjunto de resultados e deve ser a primeira instrução no lote.  
  
-   Se o conjunto de resultados usar associações de resultado, as consultas devem retornar o mesmo número de colunas. Se as consultas retornarem um número diferente de colunas, a tarefa falhará. Porém, mesmo que a tarefa falhe, as consultas executadas, como DELETE ou INSERT, podem ser executadas com êxito.  
  
-   Se as associações de resultado usarem nomes de coluna, a consulta deve retornar colunas que tenham os mesmos nomes do conjunto de resultados usado na tarefa. Se as colunas estiverem ausentes, a tarefa falhará.  
  
-   Se a tarefa usar associações de parâmetro, todas as consultas do lote devem ter o mesmo número e os mesmos tipos de parâmetros.  
  
## <a name="run-parameterized-sql-commands"></a>Executar comandos SQL parametrizados  
 As instruções SQL e os procedimentos armazenados frequentemente usam parâmetros de entrada, parâmetros de saída e códigos de retorno. A tarefa Execute SQL dá suporte aos tipos de parâmetro **Input**, **Output**e **ReturnValue** . Use o tipo **Input** para parâmetros de entrada, **Output** para parâmetros de saída e **ReturnValue** para códigos de retorno.  
  
> [!NOTE]  
>  Você só poderá usar parâmetros em uma tarefa Executar SQL se o provedor de dados der suporte a eles.  
  
## <a name="specify-a-result-set-type"></a>Especificar um tipo de conjunto de resultados  
 Dependendo do tipo de comando SQL, um conjunto de resultados pode ou não ser retornado para a tarefa Executar SQL. Por exemplo, uma instrução SELECT normalmente retorna um conjunto de resultados, mas uma instrução INSERT não. O conjunto de resultados de uma instrução SELECT pode conter nenhuma linha, uma linha ou muitas linhas. Os procedimentos armazenados também podem retornar um valor inteiro, chamado de código de retorno, para indicar o status de execução do procedimento. Nesse caso, o conjunto de resultados consiste em uma única linha.  
  
## <a name="configure-the-execute-sql-task"></a>Configurar a tarefa Executar SQL  
 Você pode configurar a tarefa Executar SQL das seguintes formas:  
  
-   Especifique o tipo de gerenciador de conexões a ser usado para conectar-se a um banco de dados.  
  
-   Especifique o tipo de conjunto de resultados retornado pela instrução SQL.  
  
-   Especifique um tempo limite para as instruções SQL.  
  
-   Especifique a origem da instrução SQL.  
  
-   Indique se a tarefa ignora a fase de preparação para a instrução SQL.  
  
-   Se você usar o tipo de conexão ADO, indique se a instrução SQL é um procedimento armazenado. Para outros tipos de conexão, essa propriedade é somente leitura e seu valor é sempre **falso**.  
  
 Você pode definir propriedades programaticamente ou por meio do Designer [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  

## <a name="general-page---execute-sql-task-editor"></a>Página Geral – Editor da Tarefa Executar SQL
 Use a página **Geral** da caixa de diálogo **Editor da Tarefa Executar SQL** para configurar a tarefa Executar SQL e fornecer a instrução SQL executada pela tarefa.  

Para saber mais sobre a linguagem de consulta Transact-SQL, consulte [Referência de Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/transact-sql-reference-database-engine.md).  
  
### <a name="static-options"></a>Opções estáticas  
 **Nome**  
 Forneça um nome exclusivo para a tarefa Executar SQL no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a tarefa Executar SQL. Como prática recomendável, para tornar os pacotes autodocumentados e mais fáceis de manter, descreva a tarefa de acordo com a sua finalidade.  
  
 **TimeOut**  
 Especifique o número máximo de segundos que a tarefa será executada antes de exceder o tempo limite. O valor 0 indica que não há limite de tempo. O padrão é 0.  
  
> [!NOTE]  
>  Procedimentos armazenados não atingirão o tempo limite se emularem uma funcionalidade de suspensão fornecendo um tempo para que as conexões sejam estabelecidas e as transações completadas sejam maior que o número de segundos especificados pelo **TimeOut**. Porém, os procedimentos armazenados que executam as consultas estão sempre sujeitos à restrição de tempo especificada pelo **TimeOut**.  
  
 **CodePage**  
 Especifique a página de código a ser usada ao converter valores Unicode em variáveis. O valor padrão é a página de código do computador local.  
  
> [!NOTE]  
>  Quando a tarefa Executar SQL usa um gerenciador de conexões ADO ou ODBC, a propriedade **CodePage** não fica disponível. Se a sua solução requer o uso de uma página de código, utilize um gerenciador de conexões OLE DB ou ADO.NET com a tarefa Executar SQL.  
  
 **TypeConversionMode**  
 Quando você definir essa propriedade como **Allowed**, a Tarefa Executar SQL tentará converter o parâmetro de saída e os resultados da consulta no tipo de dados da variável à qual os resultados estão atribuídos. Isso se aplica ao tipo de conjunto de resultados de **Linha única** .  
  
 **ResultSet**  
 Especifique o tipo de resultado esperado pela instrução SQL que está sendo executada. Escolha entre **Linha Simples**, **Conjunto de Resultados Completo**, **XML**, ou **Nenhum**.  
  
 **ConnectionType**  
 Escolha o tipo de gerenciador de conexões a ser usado para conectar-se à fonte de dados. Os tipos de conexão disponíveis incluem **OLE DB**, **ODBC**, **ADO**, **ADO.NET** e **SQLMOBILE**.  
  
 **Tópicos relacionados:** [Gerenciador de conexões do OLE DB](../../integration-services/connection-manager/ole-db-connection-manager.md)e [Gerenciador de conexões ODBC](../../integration-services/connection-manager/odbc-connection-manager.md)e [Gerenciador de conexões ADO](../../integration-services/connection-manager/ado-connection-manager.md)e [Gerenciador de conexões ADO.NET](../../integration-services/connection-manager/ado-net-connection-manager.md)e [Gerenciador de conexões do SQL Server Compact Edition](../../integration-services/connection-manager/sql-server-compact-edition-connection-manager.md)  
  
 **Conexão**  
 Escolha a conexão a partir de uma lista definida de gerenciadores de conexões. Para criar uma nova conexão, selecione \<**Nova conexão…**>.  
  
 **SQLSourceType**  
 Selecione o tipo de origem da instrução SQL que a tarefa executa.  
  
 Dependendo do tipo de gerenciador de conexões que a tarefa Executar SQL utiliza, você deve usar marcadores de parâmetro específicos em instruções SQL com parâmetros.    
  
 As opções dessa propriedade são listadas na tabela a seguir.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Entrada Direta**|Defina a fonte como uma instrução Transact-SQL. Selecionando esse valor, a opção dinâmica **Instrução SQL**é exibida.|  
|**Conexão do Arquivo**|Selecione um arquivo que contém uma instrução Transact-SQL. Definindo essa opção, a opção dinâmica **FileConnection**é exibida.|  
|**Variável**|Defina a fonte como uma variável que identifique a instrução Transact-SQL. Selecionando esse valor, a opção dinâmica **SourceVariable**é exibida.|  
  
 **QueryIsStoredProcedure**  
 Indica se a instrução SQL especificada a ser executada é um procedimento armazenado. Essa propriedade será de somente leitura/gravação se a tarefa usar o gerenciador de conexões ADO. Caso contrário a propriedade será somente leitura e seu valor será **false**.  
  
 **BypassPrepare**  
 Indique se a instrução SQL está preparada.  **true** ignora a preparação; **false** prepara a instrução SQL antes de executá-la. Essa opção só está disponível com conexões OLE DB que dão suporte à preparação.  
  
 **Tópicos relacionados:**  [Execução preparada](../../relational-databases/native-client-odbc-queries/executing-statements/prepared-execution.md)  
  
 **Procurar**  
 Localize um arquivo que contém uma instrução SQL usando a caixa de diálogo **Abrir** . Selecione um arquivo para copiar o conteúdo do arquivo como uma instrução SQL para a propriedade **SQLStatement** .  
  
 **Construir Consulta**  
 Crie uma instrução SQL usando a caixa de diálogo **Construtor de Consultas** , uma ferramenta gráfica usada para criar consultas. Esta opção está disponível quando a opção **SQLSourceType** é definida como **Entrada Direta**.  
  
 **Analisar Consulta**  
 Valide a sintaxe da instrução SQL.  
  
### <a name="sqlsourcetype-dynamic-options"></a>Opções dinâmicas SQLSourceType  
  
#### <a name="sqlsourcetype--direct-input"></a>SQLSourceType = Entrada direta  
 **SQLStatement**  
 Digite a instrução SQL a ser executada na caixa de opções ou clique no botão Procurar (...) para digitar a instrução SQL na caixa de diálogo **Inserir Consulta SQL** ou clique em **Construir Consulta** para redigir a instrução usando a caixa de diálogo **Construtor de Consultas**.  
  
 **Tópicos relacionados:** [Construtor de Consultas](https://msdn.microsoft.com/library/780752c9-6e3c-4f44-aaff-4f4d5e5a45c5)  
  
#### <a name="sqlsourcetype--file-connection"></a>SQLSourceType = Conexão do Arquivo  
 **FileConnection**  
 Selecione um gerenciador de conexões de arquivos existente ou clique em \<**Nova conexão...**> para criar um novo gerenciador de conexões.  
  
 **Tópicos relacionados:** [Gerenciador de conexões de arquivos](../../integration-services/connection-manager/file-connection-manager.md), [Editor do Gerenciador de conexões de Arquivos](../../integration-services/connection-manager/file-connection-manager-editor.md)  
  
#### <a name="sqlsourcetype--variable"></a>SQLSourceType = Variável  
 **SourceVariable**  
 Selecione uma variável existente ou clique em \<**Nova variável...**> para criar uma nova variável.  
  
 **Tópicos relacionados:** [Variáveis do Integration Services &#40;SSIS&#41;](../../integration-services/integration-services-ssis-variables.md), [Adicionar variável](https://msdn.microsoft.com/library/d09b5d31-433f-4f7c-8c68-9df3a97785d5)  
 
## <a name="parameter-mapping-page---execute-sql-task-editor"></a>Página Mapeamento de Parâmetros – Editor da Tarefa Executar SQL
Use a página **Mapeamento de Parâmetros** da caixa de diálogo **Editor da Tarefa Executar SQL** para mapear as variáveis para os parâmetros na instrução SQL.  
  
### <a name="options"></a>Opções  
 **Nome da Variável**  
 Depois de adicionar um mapeamento de parâmetros clicando em **Adicionar**, selecione uma variável de sistema ou definida pelo usuário na lista ou clique em \<**Nova variável...**> para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**.  
  
 **Tópicos relacionados:** [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md)  
  
 **Direção**  
 Selecione a direção do parâmetro. Mapeie cada variável para um parâmetro de entrada, parâmetro de saída ou um código de retorno.  
  
 **Tipo de Dados**  
 Selecione o tipo de dados do parâmetro. A lista de tipos de dados disponíveis é específica para o provedor selecionado no gerenciador de conexões usado pela tarefa.  
  
 **Nome do parâmetro**  
 Forneça um nome de parâmetro.  
  
 Dependendo do tipo de gerenciador de conexões usado pela tarefa, você deve usar números ou nomes de parâmetro. Alguns tipos de gerenciadores de conexões exigem que o primeiro caractere do nome do parâmetro seja o sinal \@, nomes específicos como \@Param1, ou nomes de coluna como nomes de parâmetro.  
  
 **Tamanho do Parâmetro**  
 Informe o tamanho dos parâmetros com comprimento variável, como cadeias de caracteres e campos binários.  
  
 Esta configuração garante que o provedor aloque espaço suficiente para obter valores de parâmetro de comprimento variável.  
  
 **Adicionar**  
 Clique para adicionar um mapeamento de parâmetros.  
  
 **Remover**  
 Selecione um mapeamento de parâmetros na lista e clique em **Remover**.  
 
## <a name="result-set-page---execute-sql-task-editor"></a>Página Conjunto de Resultados – Editor da Tarefa Executar SQL
Use a página **Conjunto de Resultados** da caixa de diálogo **Editor da Tarefa Executar SQL** para mapear o resultado da instrução SQL para variáveis novas ou já existentes. As opções dessa caixa de diálogo serão desabilitadas se o **ResultSet** na página Geral for definido como **Nenhum**.  
  
### <a name="options"></a>Opções  
 **Nome do Resultado**  
 Depois que você adicionar um conjunto de resultados de conjunto de mapeamento clicando em **Adicionar**, forneça um nome exclusivo para o resultado. Dependendo do tipo de conjunto de resultados, é necessário usar nomes de resultado específicos.  
  
 Se o tipo de conjunto de resultados for **Linha única**, será possível usar o nome de uma coluna retornado pela consulta ou o número que representam a posição de uma coluna na lista de colunas de uma coluna retornada pela consulta.  
  
 Se o tipo de conjunto de resultados for **Conjunto de resultados completo** ou **XML**, será necessário usar 0 como o nome de conjunto de resultados.  
 
  
 **Nome da Variável**  
 Mapeie o conjunto de resultados para uma variável selecionando uma variável ou clique em \<**Nova variável...**> para adicionar uma nova variável usando a caixa de diálogo **Adicionar Variável**.  
  
 **Adicionar**  
 Clique para adicionar um mapeamento de conjunto de resultados.  
  
 **Remover**  
 Selecione um mapeamento de conjunto de resultados na lista e clique em **Remover**.  
 
## <a name="parameters-in-the-execute-sql-task"></a>Parâmetros na Tarefa Executar SQL
As instruções SQL e os procedimentos armazenados frequentemente usam parâmetros **input** , parâmetros **output** e códigos de retorno. No [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], a tarefa Execute SQL dá suporte aos tipos de parâmetro **Input**, **Output** e **ReturnValue**. Use o tipo **Input** para parâmetros de entrada, **Output** para parâmetros de saída e **ReturnValue** para códigos de retorno.  
  
> [!NOTE]  
>  Você só poderá usar parâmetros em uma tarefa Executar SQL se o provedor de dados der suporte a eles.  
  
 Os parâmetros em comandos SQL, inclusive consultas e procedimentos armazenados, são mapeados para variáveis definidas pelo usuário criadas no escopo da tarefa Executar SQL, um contêiner pai ou no escopo do pacote. Os valores das variáveis podem ser definidos em tempo de projeto ou populados dinamicamente em tempo de execução. Você também pode mapear parâmetros para variáveis de sistema. Para obter mais informações, consulte [Variáveis do SSIS &#40;Integration Services&#41;](../../integration-services/integration-services-ssis-variables.md) e [Variáveis do Sistema](../../integration-services/system-variables.md).  
  
 No entanto, trabalhar com parâmetros e códigos de retorno em uma tarefa Executar SQL é mais do que apenas saber para quais tipos de parâmetro a tarefa tem suporte e como esses parâmetros serão mapeados. Há requisitos de uso adicionais e diretrizes para usar parâmetros e códigos de retorno de modo bem-sucedido na tarefa Executar SQL. Esses requisitos de uso e diretrizes são abordados no restante deste tópico:  
  
-   [Usando nomes e marcadores de parâmetros](#Parameter_names_and_markers)  
  
-   [Usando parâmetros com tipos de dados de data e hora](#Date_and_time_data_types)  
  
-   [Usando parâmetros em cláusulas WHERE](#WHERE_clauses)  
  
-   [Usando parâmetros com procedimentos armazenados](#Stored_procedures)  
  
-   [Obtendo valores de códigos de retorno](#Return_codes)    
  
###  <a name="Parameter_names_and_markers"></a> Marcadores e nomes de parâmetro  
 Dependendo do tipo de conexão usado pela tarefa Executar SQL, a sintaxe do comando SQL utiliza marcadores de parâmetro diferentes. Por exemplo, o tipo de gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] exige que o comando SQL use um marcador de parâmetro no formato **\@varParameter**, enquanto que o tipo de conexão OLE DB exige o marcador de parâmetro ponto de interrogação (?).  
  
 Os nomes que você pode usar como nomes de parâmetro nos mapeamentos entre as variáveis e os parâmetros também variam por tipo de gerenciador de conexões. Por exemplo, o tipo de gerenciador de conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usa um nome definido pelo usuário com um prefixo \@, enquanto o tipo de gerenciador de conexões OLE DB requer que você use o valor numérico de ordinal de base 0 como o nome do parâmetro.  
  
 A tabela a seguir resume os requisitos de comandos SQL para os tipos de gerenciador de conexões que podem ser utilizados pela tarefa Executar SQL.  
  
|Tipo de conexão|Marcador de parâmetro|Nome do parâmetro|Exemplo de comando SQL|  
|---------------------|----------------------|--------------------|-------------------------|  
|ADO|?|Param1, Param2, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|\@\<nome do parâmetro>|\@\<nome do parâmetro>|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = \@parmContactID|  
|ODBC|?|1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
|EXCEL e OLE DB|?|0, 1, 2, 3, ...|SELECT FirstName, LastName, Title FROM Person.Contact WHERE ContactID = ?|  
  
#### <a name="use-parameters-with-adonet-and-ado-connection-managers"></a>Usar parâmetros com os gerenciadores de conexões ADO.NET e ADO  
 Gerenciadores de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] e ADO têm requisitos específicos para comandos SQL que usam parâmetros:  
  
-   Gerenciadores de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] requerem que o comando SQL use nomes de parâmetro como marcadores de parâmetro. Isso significa que as variáveis podem ser mapeadas diretamente para parâmetros. Por exemplo, a variável `@varName` é mapeada para o parâmetro denominado `@parName` e fornece um valor para o parâmetro `@parName`.  
  
-   Os gerenciadores de conexões ADO requerem que o comando SQL use pontos de interrogação (?) como marcadores de parâmetro. No entanto, você pode usar qualquer nome definido pelo usuário, com exceção de valores de número inteiro, como nomes de parâmetro.  
  
 Para fornecer valores a parâmetros, as variáveis são mapeadas para nomes de parâmetro. Em seguida, a tarefa Executar SQL usa o valor ordinal do nome do parâmetro na lista de parâmetros para carregar valores de variáveis a parâmetros.  
  
#### <a name="use-parameters-with-excel-odbc-and-ole-db-connection-managers"></a>Usar parâmetros com os gerenciadores de conexões EXCEL, ODBC e OLE DB  
 Os gerenciadores de conexões EXCEL, ODBC e OLE DB requerem que o comando SQL use pontos de interrogação (?) como marcadores de parâmetro e valores numéricos de base 0 ou base 1 como nomes de parâmetros. Se a tarefa Executar SQL utilizar o gerenciador de conexões ODBC, o nome do parâmetro mapeado para o primeiro parâmetro na consulta será denominado 1; caso contrário, o parâmetro será denominado 0. Para os parâmetros subsequentes, o valor numérico do nome do parâmetro indica o parâmetro no comando SQL para o qual o nome do parâmetro é mapeado. Por exemplo, o parâmetro denominado 3 é mapeado para o terceiro parâmetro, que é representado pelo terceiro ponto de interrogação (?) no comando SQL.  
  
 Para fornecer valores a parâmetros, as variáveis são mapeadas para nomes de parâmetros e a tarefa Executar SQL usa o valor ordinal do nome do parâmetro para carregar valores de variáveis a parâmetros.  
  
 Dependendo do provedor utilizado pelo gerenciador de conexões, alguns tipos de dados OLE DB talvez não tenham suporte. Por exemplo, o driver do Excel reconhece apenas um conjunto limitado de tipos de dados. Para obter mais informações sobre o comportamento do provedor Jet com o driver do Excel, consulte [Origem do Excel](../../integration-services/data-flow/excel-source.md).  
  
#### <a name="use-parameters-with-ole-db-connection-managers"></a>Usar parâmetros com gerenciadores de conexões OLE DB  
 Quando a tarefa Executar SQL usa o gerenciador de conexões OLE DB, a propriedade BypassPrepare da tarefa está disponível. Defina esta propriedade como **true** se a tarefa Executar SQL usar instruções SQL com parâmetros.  
  
 Quando você usa um gerenciador de conexões OLE DB, não pode usar subconsultas com parâmetros, porque a tarefa Executar SQL não pode derivar informações de parâmetro por meio do provedor OLE DB. Entretanto, você pode usar uma expressão para concatenar os valores de parâmetro na cadeia de caracteres de consulta de definir a propriedade SqlStatementSource da tarefa.  
  
###  <a name="Date_and_time_data_types"></a> Usar parâmetros com tipos de dados de data e hora  
  
#### <a name="use-date-and-time-parameters-with-adonet-and-ado-connection-managers"></a>Usar parâmetros de data e hora com os gerenciadores de conexões ADO.NET e ADO  
 Ao ler dados de tipos [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **time** e **datetimeoffset**, uma tarefa Executar SQL que usa um [!INCLUDE[vstecado](../../includes/vstecado-md.md)] ou o gerenciador de conexão ADO tem os seguintes requisitos adicionais:  
  
-   Em dados de **time**, um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] requer que esses dados sejam armazenados em um parâmetro cujo tipo é **Input** ou **Output** e cujo tipo de dados é **string**.  
  
-   Para dados de **datetimeoffset**, um gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)] requer que esses dados sejam armazenados em um dos seguintes parâmetros:  
  
    -   Um parâmetro cujo tipo é **Input** e cujo tipo de dados é **string**.  
  
    -   Um parâmetro cujo tipo é **Output** ou **ReturnValue**e cujo tipo de dados é **datetimeoffset**, **string**ou **datetime2**. Se você selecionar um parâmetro cujo tipo de dados é **string** ou **datetime2**, [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] converterá os dados em string ou datetime2.  
  
-   Um gerenciador de conexões ADO requer que os dados **time** ou **datetimeoffset** sejam armazenados em um parâmetro cujo tipo é **Input** ou **Output** e cujo tipo de dados é **adVarWchar**.  
  
 Para obter mais informações sobre tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e como eles são associados a tipos de dados [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Tipos de dados &#40;Transact-SQL&#41;](../../t-sql/data-types/data-types-transact-sql.md) e [Tipos de dados do Integration Services](../../integration-services/data-flow/integration-services-data-types.md).  
  
#### <a name="use-date-and-time-parameters-with-ole-db-connection-managers"></a>Usar parâmetros de data e hora com os gerenciadores de conexões OLE DB  
 Quando você usa um gerenciador de conexões OLE DB, uma tarefa Executar SQL tem requisitos de armazenamento específicos para os dados nos tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **date**, **time**, **datetime**, **datetime2**e **datetimeoffset**. Você deve armazenar estes dados em um dos tipos de parâmetros seguintes:  
  
-   Um parâmetro de entrada do tipo de dados NVARCHAR.  
  
-   Um parâmetro de saída com o tipo de dados apropriado, como listado na tabela a seguir.  
  
    |Tipo de parâmetro **Output**|Tipo de dados de data|  
    |-------------------------------|--------------------|  
    |DBDATE|**date**|  
    |DBTIME2|**time**|  
    |DBTIMESTAMP|**datetime**, **datetime2**|  
    |DBTIMESTAMPOFFSET|**datetimeoffset**|  
  
 Se os dados não forem armazenados no parâmetro de entrada ou saída apropriado, o pacote falhará.  
  
#### <a name="use-date-and-time-parameters-with-odbc-connection-managers"></a>Usar parâmetros de data e hora com os gerenciadores de conexões ODBC  
 Quando você usa um gerenciador de conexões ODBC, uma tarefa Executar SQL tem requisitos de armazenamento específicos para dados com um dos tipos de dados [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , **date**, **time**, **datetime**, **datetime2**ou **datetimeoffset**. Você deve armazenar estes dados em um dos tipos de parâmetros seguintes:  
  
-   Um parâmetro **input** do tipo de dados SQL_WVARCHAR  
  
-   Um parâmetro **output** com o tipo de dados apropriado, como listado na tabela a seguir.  
  
    |Tipo de parâmetro**Output** |Tipo de dados de data|  
    |-------------------------------|--------------------|  
    |SQL_DATE|**date**|  
    |SQL_SS_TIME2|**time**|  
    |SQL_TYPE_TIMESTAMP<br /><br /> -ou-<br /><br /> SQL_TIMESTAMP|**datetime**, **datetime2**|  
    |SQL_SS_TIMESTAMPOFFSET|**datetimeoffset**|  
  
 Se os dados não forem armazenados no parâmetro de entrada ou saída apropriado, o pacote falhará.  
  
###  <a name="WHERE_clauses"></a> Usar parâmetros em cláusulas WHERE  
 Os comandos SELECT, INSERT, UPDATE e DELETE frequentemente incluem cláusulas WHERE para especificar filtros que definem as condições que cada linha nas tabelas de origem devem atender para se qualificar para um comando SQL. Os parâmetros fornecem os valores de filtro nas cláusulas WHERE.  
  
 Você pode usar marcadores de parâmetro para fornecer valores de parâmetros dinamicamente. As regras para quais marcadores e nomes de parâmetros podem ser usados na instrução SQL dependem do tipo de gerenciador de conexões utilizado por Executar SQL.  
  
 A tabela a seguir lista exemplos do comando SELECT por tipo de gerenciador de conexões. As instruções INSERT, UPDATE e DELETE são semelhantes. Os exemplos usam SELECT para retornar produtos da tabela **Produto** em [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] que tenham uma **ProductID** maior e menor que os valores especificados pelos dois parâmetros.  
  
|Tipo de conexão|Sintaxe de SELECT|  
|---------------------|-------------------|  
|EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
  
 Os exemplos exigiriam parâmetros que têm os seguintes nomes:  
  
-   Os gerenciadores de conexões EXCEL e OLED DB usam os nomes de parâmetro 0 e 1. O tipo de conexão ODBC usa 1 e 2.  
  
-   O tipo de conexão ADO pode usar quaisquer dois nomes de parâmetro, como Param1 e Param2, mas os parâmetros devem ser mapeados pela posição original na lista de parâmetros.  
  
-   O tipo de conexão [!INCLUDE[vstecado](../../includes/vstecado-md.md)] usa os nomes de parâmetro \@parmMinProductID e \@parmMaxProductID.  
  
###  <a name="Stored_procedures"></a> Usar parâmetros com procedimentos armazenados  
 Os comandos SQL que executam procedimentos armazenados também podem usar mapeamento de parâmetro. As regras de como usar marcadores e nomes de parâmetros dependem do tipo de gerenciador de conexões utilizado por Executar SQL, assim como as regras para consultas parametrizadas.  
  
 A tabela a seguir lista exemplos do comando EXEC por tipo de gerenciador de conexões. Os exemplos executam o procedimento armazenado **uspGetBillOfMaterials** em [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)]. O procedimento armazenado usa os parâmetros `@StartProductID` e `@CheckDate` **e** .  
  
|Tipo de conexão|Sintaxe de EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC uspGetBillOfMaterials ?, ?`|  
|ODBC|`{call uspGetBillOfMaterials(?, ?)}`<br /><br /> Para obter mais informações sobre a sintaxe de chamada ODBC, consulte o tópico [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462) (Parâmetros de procedimento) na Referência do programador de ODBC na Biblioteca MSDN.|  
|ADO|Se IsQueryStoredProcedure estiver definido como **False**, `EXEC uspGetBillOfMaterials ?, ?`<br /><br /> Se IsQueryStoredProcedure for definido como **True**, `uspGetBillOfMaterials`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Se IsQueryStoredProcedure estiver definido como **False**, `EXEC uspGetBillOfMaterials @StartProductID, @CheckDate`<br /><br /> Se IsQueryStoredProcedure for definido como **True**, `uspGetBillOfMaterials`|  
  
 Para usar parâmetros de saída, a sintaxe requer que a palavra-chave OUTPUT seja colocada após cada marcador de parâmetro. Por exemplo, a sintaxe do parâmetro de saída a seguir está correta: `EXEC myStoredProcedure ? OUTPUT`.  
  
 Para obter mais informações sobre como usar parâmetros de entrada e saída com procedimentos armazenados Transact-SQL, consulte [EXECUTE &#40;Transact-SQL&#41;](../../t-sql/language-elements/execute-transact-sql.md).  
 
### <a name="map-query-parameters-to-variables"></a>Mapear parâmetros para variáveis
Esta seção descreve como usar uma instrução SQL parametrizada na tarefa Executar SQL e criar mapeamentos entre variáveis e os parâmetros na instrução SQL.  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] com o qual você deseja trabalhar.  
  
2.  No Gerenciador de Soluções, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Se o pacote ainda não incluir uma tarefa Executar SQL, adicione uma ao fluxo de controle do pacote. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Clique duas vezes na tarefa Executar SQL.  
  
6.  Forneça um comando SQL parametrizado de um dos seguintes modos:  
  
    -   Use a entrada direta e digite o comando SQL na propriedade SQLStatement.  
  
    -   Use a entrada direta, clique em **Construir Consulta**e crie um comando SQL usando as ferramentas gráficas que o Construtor de Consultas fornece.  
  
    -   Use uma conexão de arquivo e depois faça referência ao arquivo que contém o comando SQL.  
  
    -   Use uma variável e depois faça referência à variável que contém o comando SQL.  
  
     Os marcadores de parâmetros que você usa nas instruções SQL parametrizadas dependem do tipo de conexão que a tarefa Executar SQL usa.  
  
    |Tipo de conexão|Marcador de parâmetro|  
    |---------------------|----------------------|  
    |ADO|?|  
    |ADO.NET e SQLMOBILE|\@\<nome do parâmetro>|  
    |ODBC|?|  
    |EXCEL e OLE DB|?|  
  
     A tabela a seguir lista exemplos do comando SELECT por tipo de gerenciador de conexões. Os parâmetros fornecem os valores de filtro nas cláusulas WHERE. Os exemplos usam SELECT para retornar produtos da tabela **Produto** em [!INCLUDE[ssSampleDBUserInputNonLocal](../../includes/sssampledbuserinputnonlocal-md.md)] que tenham uma **ProductID** maior e menor que os valores especificados pelos dois parâmetros.  
  
    |Tipo de conexão|Sintaxe de SELECT|  
    |---------------------|-------------------|  
    |EXCEL, ODBC e OLEDB|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |ADO|`SELECT* FROM Production.Product WHERE ProductId > ? AND ProductID < ?`|  
    |[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|`SELECT* FROM Production.Product WHERE ProductId > @parmMinProductID AND ProductID < @parmMaxProductID`|  
   
7.  Clique em **Mapeamento de Parâmetro**.  
  
8.  Para adicionar um mapeamento de parâmetro, clique em **Adicionar**.  
  
9. Forneça um nome na caixa **Nome do Parâmetro** .  
  
     Os nomes de parâmetros que você usa dependem do tipo de conexão que a tarefa Executar SQL usa.  
  
    |Tipo de conexão|Nome do Parâmetro|  
    |---------------------|--------------------|  
    |ADO|Param1, Param2, ...|  
    |ADO.NET e SQLMOBILE|\@\<nome do parâmetro>|  
    |ODBC|1, 2, 3, ...|  
    |EXCEL e OLE DB|0, 1, 2, 3, ...|  
  
10. Na lista **Nome da Variável** , selecione uma variável. Para obter mais informações, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
11. Na lista **Direção** , especifique se o parâmetro é uma entrada, uma saída ou um valor de retorno.  
  
12. Na lista **Tipo de Dados** , defina o tipo de dados do parâmetro.  
  
    > [!IMPORTANT]  
    >  O tipo de dados do parâmetro deve ser compatível com o tipo de dados da variável.  
  
13. Repita as etapas de 8 a 11 para cada parâmetro na instrução SQL.  
  
    > [!IMPORTANT]  
    >  A ordem dos mapeamentos de parâmetros deve ser igual à ordem em que os parâmetros aparecem na instrução SQL.  
  
14. Clique em **OK**.  

##  <a name="Return_codes"></a> Obter os valores de códigos de retorno  
 Um procedimento armazenado pode retornar um valor inteiro chamado código de retorno para indicar o status de execução de um procedimento. Para implementar códigos de retorno na tarefa Executar SQL, use parâmetros do tipo **ReturnValue** .  
  
 A tabela a seguir lista, por tipo de conexão, alguns exemplos de comandos EXEC que implementam códigos de retorno. Todos os exemplos usam um parâmetro **input** . As regras de uso de marcadores e nomes de parâmetro são as mesmas para todos os tipos de parâmetros: **Input**, **Output** e **ReturnValue**.  
  
 Algumas sintaxes não dão suporte a literais de parâmetro. Nesse caso, você deve fornecer o valor dó parâmetro usando uma variável.  
  
|Tipo de conexão|Sintaxe de EXEC|  
|---------------------|-----------------|  
|EXCEL e OLEDB|`EXEC ? = myStoredProcedure 1`|  
|ODBC|`{? = call myStoredProcedure(1)}`<br /><br /> Para obter mais informações sobre a sintaxe de chamada ODBC, consulte o tópico [Procedure Parameters](https://go.microsoft.com/fwlink/?LinkId=89462) (Parâmetros de procedimento) na Referência do programador de ODBC na Biblioteca MSDN.|  
|ADO|Se IsQueryStoreProcedure estiver definido como **False**, `EXEC ? = myStoredProcedure 1`<br /><br /> Se IsQueryStoreProcedure estiver definido como **True**, `myStoredProcedure`|  
|[!INCLUDE[vstecado](../../includes/vstecado-md.md)]|Se IsQueryStoreProcedure for definido como **True**.<br /><br /> `myStoredProcedure`|  
  
 Na sintaxe mostrada na tabela anterior, a tarefa Executar SQL usa o tipo de fonte **Entrada Direta** para executar o procedimento armazenado. A tarefa Executar SQL também pode usar o tipo de fonte **Conexão de Arquivo** para executar um procedimento armazenado. Independentemente de a tarefa Executar SQL usar o tipo de origem **Entrada Direta** ou **Conexão de Arquivo** , use um parâmetro do tipo **ReturnValue** para implementar o código de retorno.
  
 Para obter mais informações sobre como usar códigos de retorno com procedimentos armazenados Transact-SQL, consulte [RETURN &#40;Transact-SQL&#41;](../../t-sql/language-elements/return-transact-sql.md).  
  
## <a name="result-sets-in-the-execute-sql-task"></a>Conjuntos de resultados na tarefa Executar SQL
 Em um pacote do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , se um conjunto de resultados será retornado à tarefa Executar SQL dependerá do tipo de comando SQL usado pela tarefa. Por exemplo, uma instrução SELECT normalmente retorna um conjunto de resultados, mas uma instrução INSERT não.  
  
 O que o conjunto de resultados contém também varia com o comando SQL. Por exemplo, o conjunto de resultados de uma instrução SELECT pode conter nenhuma linha, uma linha ou muitas linhas. No entanto, o conjunto de resultados de uma instrução SELECT que retorna uma contagem ou soma tem apenas uma única linha.  
  
 Trabalhar com conjuntos de resultados em uma tarefa Executar SQL é mais do que apenas saber se o comando SQL retorna um conjunto de resultados e o que ele contém. Há requisitos de uso e diretrizes adicionais para a utilização bem-sucedida dos conjuntos de resultados na tarefa Executar SQL. Esses requisitos de uso e diretrizes são abordados no restante deste tópico:  
  
-   [Especificando um tipo de conjunto de resultados](#Result_set_type)  
  
-   [Popular uma variável com um conjunto de resultados](#Populate_variable_with_result_set)  
  
###  <a name="Result_set_type"></a> Especificar um tipo de conjunto de resultados  
 O a tarefa Executar SQL dá suporte aos seguintes tipos de conjuntos de resultados:  
  
-   O conjunto de resultados **Nenhum** é usado quando a consulta não retorna nenhum resultado. Por exemplo, esse conjunto de resultados é usado para consultas que adicionam, alteram e excluem registros em uma tabela.  
  
-   O conjunto de resultados **Linha simples** é usado quando a consulta retorna apenas uma linha. Por exemplo, esse conjunto de resultados é usado para uma instrução SELECT que retorna uma contagem ou soma.  
  
-   O **Conjunto de resultados completo** é usado quando a consulta retorna várias linhas. Por exemplo, este conjunto de resultados é usado para uma instrução SELECT que recupera todas as linhas em uma tabela.  
  
-   O conjunto de resultados **XML** é usado quando a consulta retorna um conjunto de resultados em um formato XML. Por exemplo, esse conjunto de resultados é usado para uma instrução SELECT que inclui uma cláusula FOR XML.  
  
 Se a tarefa Executar SQL usar o **Conjunto de resultados completo** e a consulta retornar vários conjuntos de linhas, a tarefa retornará apenas o primeiro. Se este conjunto de linhas gerar um erro, a tarefa informará o erro. Se outros conjuntos de linhas gerarem erros, a tarefa não os informará.  
  
###  <a name="Populate_variable_with_result_set"></a> Popular uma variável com um conjunto de resultados  
 Você poderá associar o conjunto de resultados retornado por uma consulta a uma variável definida pelo usuário se o tipo de conjunto de resultados for uma única linha, um conjunto de linhas ou XML.  
  
 Se o tipo de conjunto resultante for **Linha simples**, você poderá associar uma coluna no resultado de retorno a uma variável usando o nome da coluna como o nome do conjunto de resultados ou pode usar a posição ordinal da coluna na lista de colunas como o nome do conjunto de resultados. Por exemplo, o nome do conjunto de resultados da consulta `SELECT Color FROM Production.Product WHERE ProductID = ?` pode ser **Color** ou **0**. Se a consulta retornar várias colunas e você quiser acessar os valores em todas elas, associe cada coluna a uma variável diferente. Se você mapear as colunas para variáveis usando números como nomes do conjunto de resultados, os números refletirão a ordem em que as colunas aparecerão na lista de colunas da consulta. Por exemplo, na consulta `SELECT Color, ListPrice, FROM Production.Product WHERE ProductID = ?`, você usa 0 para a coluna **Color** e 1 para a coluna **ListPrice** . A capacidade de usar um nome de coluna como o nome do conjunto de resultados depende do provedor que a tarefa está configurada para usar. Nem todos os provedores tornam os nomes das colunas disponíveis.  
  
 Algumas consultas que retornam um único valor podem não incluir nomes de colunas. Por exemplo, a instrução `SELECT COUNT (*) FROM Production.Product` não retorna nenhum nome de coluna. Você pode acessar o resultado de retorno usando a posição ordinal, 0, como o nome do resultado. Para acessar o resultado de retorno por nome de coluna, a consulta deve incluir uma cláusula AS \<nome do alias> para fornecer um nome de coluna. A instrução `SELECT COUNT (*)AS CountOfProduct FROM Production.Product`fornece a coluna **CountOfProduct** . Você pode acessar a coluna de resultado de retorno que usa o nome de coluna **CountOfProduct** ou a posição ordinal 0.  
  
 Se o tipo de conjunto de resultados for **Conjunto de resultados completo** ou **XML**, será necessário usar 0 como o nome de conjunto de resultados.  
  
 Quando você mapeia uma variável para um conjunto de resultados com o tipo de conjunto de resultados **Linha simples** , a variável deve ter um tipo de dados compatível com o tipo de dados da coluna que o conjunto de resultados contém. Por exemplo, um conjunto de resultados que contém uma coluna com um tipo de dados **String** não pode ser mapeado para uma variável com um tipo de dados numérico. Quando você define a propriedade **TypeConversionMode** como **Allowed**, a Tarefa Executar SQL tentará converter o parâmetro de saída e os resultados da consulta no tipo de dados da variável à qual os resultados estão atribuídos.  
  
 Um conjunto de resultados XML somente pode ser mapeado para uma variável com o tipo de dados **String** ou **Object** . Se a variável tiver o tipo de dados **String** , a tarefa Executar SQL retorna uma cadeia de caracteres e a fonte XML pode consumir os dados XML. Se a variável tiver o tipo de dados **Object** , a tarefa Executar SQL retornará um objeto do Modelo de Objeto do Documento (DOM).  
  
 Um **Conjunto de resultados completo** deve ser mapeado para uma variável do tipo de dados **Object** . O resultado de retorno é um objeto de conjunto de linhas. Você pode usar um contêiner do Loop Foreach para extrair os valores de linha da tabela que são armazenados na variável Object em variáveis ​​de pacote e usar uma Tarefa Script para gravar os dados armazenados em variáveis ​​de pacotes em um arquivo. Para uma demonstração de como fazer isso usando um contêiner de Loop Foreach e uma Tarefa Script, confira a amostra CodePlex, [Executar conjuntos de resultados e parâmetros SQL](https://go.microsoft.com/fwlink/?LinkId=157863), no msftisprodsamples.codeplex.com.  
  
 A tabela a seguir resume os tipos de dados de variáveis que podem ser mapeadas para conjuntos de resultados.  
  
|Tipo de conjunto de resultados|Tipo de dados da variável|Tipo de objeto|  
|---------------------|---------------------------|--------------------|  
|Linha simples|Qualquer tipo compatível com a coluna de tipo no conjunto de resultados.|Não aplicável|  
|Conjunto de resultados completo|**Objeto**|Se a tarefa usar um gerenciador de conexões nativo, incluindo os gerenciadores de conexões ADO, OLE DB, Excel e ODBC, o objeto retornado será **Recordset**ADO.<br /><br /> Se a tarefa usar um gerenciador de conexões gerenciado, como o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)], o objeto retornado será um **System.Data.DataSet**.<br /><br /> Você pode usar uma tarefa Script para acessar o objeto **System.Data.DataSet** , conforme mostrado no exemplo a seguir.<br /><br /> `Dim dt As Data.DataTable`<br /><br /> `Dim ds As Data.DataSet = CType(Dts.Variables("Recordset").Value, DataSet) dt = ds.Tables(0)`|  
|XML|**String**|**String**|  
|XML|**Objeto**|Se a tarefa usar um gerenciador de conexões nativo, inclusive os gerenciadores de conexões ADO, OLE DB, Excel e ODBC, o objeto retornado será **MSXML6.IXMLDOMDocument**.<br /><br /> Se a tarefa usar um gerenciador de conexões gerenciado, como o gerenciador de conexões [!INCLUDE[vstecado](../../includes/vstecado-md.md)], o objeto retornado será um **System.Xml.XmlDocument**.|  
  
 A variável pode ser definida no escopo da tarefa Executar SQL ou do pacote. Se a variável tiver escopo de pacote, o conjunto de resultados estará disponível para outras tarefas e contêineres no pacote e para qualquer pacote executado pelas tarefas Executar pacote ou Executar Pacotes do DTS 2000.  
  
 Quando você mapeia uma variável para um conjunto de resultados de **Linha simples** , os valores que não são de cadeia de caracteres retornados pela instrução SQL são convertidos em cadeias de caracteres quando as seguintes condições são atendidas:  
  
-   A propriedade **TypeConversionMode** é definida como verdadeira. Você define o valor da propriedade na janela Propriedades ou por meio do **Editor da Tarefa Executar SQL**.  
  
-   A conversão não resultará em truncamento de dados.  
  
## <a name="map-result-sets-to-variables-in-an-execute-sql-task"></a>Mapear conjuntos de resultados para variáveis em uma tarefa Executar SQL
Esta seção descreve como criar um mapeamento entre um conjunto de resultados e uma variável em uma tarefa Executar SQL. O mapeamento de um conjunto de resultados para uma variável disponibiliza o conjunto de resultados para outros elementos no pacote. Por exemplo, um script em uma tarefa Script pode ler a variável e usar os valores do conjunto de resultados; ou uma origem XML pode consumir o conjunto de resultados armazenado em uma variável. Se o conjunto de resultados for gerado por um pacote pai, ele poderá ser disponibilizado para um pacote filho chamado por uma tarefa Executar Pacote, mapeando o conjunto de resultados para uma variável no pacote pai e, em seguida, criando uma configuração de variável de pacote pai no pacote filho para armazenar o valor da variável pai.  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] que contém o pacote desejado.  
  
2.  No **Gerenciador de Soluções**, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Se o pacote ainda não incluir uma tarefa Executar SQL, adicione uma ao fluxo de controle do pacote. Para obter mais informações, consulte [Adicionar ou excluir uma tarefa ou um contêiner em um fluxo de controle](../../integration-services/control-flow/add-or-delete-a-task-or-a-container-in-a-control-flow.md).  
  
5.  Clique duas vezes na tarefa Executar SQL.  
  
6.  Na caixa de diálogo **Editor da Tarefa Executar SQL** , na página **Geral** , selecione o tipo do conjunto de resultados, **Linha simples**, **Conjunto de resultados completo**ou **XML** .  

7.  Clique em **Conjunto de Resultados**.  
  
8.  Para adicionar um mapeamento de conjunto de resultados, clique em **Adicionar**.  
  
9. Na lista **Nome de Variáveis** , selecione uma variável ou crie uma nova. Para obter mais informações, consulte [Adicionar, excluir, alterar o escopo de uma variável definida pelo usuário em um pacote](https://msdn.microsoft.com/library/cbf40c7f-3c8a-48cd-aefa-8b37faf8b40e).  
  
10. Na lista **Nome do Resultado** , opcionalmente, modifique o nome do conjunto de resultados.  
  
     Em geral, você pode usar o nome da coluna como o nome do conjunto de resultados ou você pode usar a posição ordinal da coluna na lista de colunas como o conjunto de resultados. A capacidade de usar um nome de coluna como o nome do conjunto de resultados depende do provedor que a tarefa está configurada para usar. Nem todos os provedores tornam os nomes das colunas disponíveis.  
  
11. Clique em **OK**.  

## <a name="troubleshoot-the-execute-sql-task"></a>Solucionar problemas da tarefa Executar SQL  
 Você pode registrar as chamadas que a tarefa Executar SQL faz para provedores de dados externos. É possível usar esse recurso de registro para solucionar problemas dos comandos SQL executados pela tarefa Executar SQL. Para registrar as chamadas que a tarefa Executar SQL faz aos provedores de dados externos, habilite o registro de pacotes e selecione o evento **Diagnóstico** no nível de pacotes. Para obter mais informações, consulte [Solucionando problemas de ferramentas para execução de pacotes](../../integration-services/troubleshooting/troubleshooting-tools-for-package-execution.md).  
  
 Às vezes um comando SQL ou procedimento armazenado retorna vários conjuntos de resultados. Esses conjuntos de resultados incluem não só conjuntos de linhas que resultam de consultas **SELECT** , mas também valores únicos que resultam de erros das instruções **RAISERROR** ou **PRINT** . A tarefa poderá ignorar ou não os erros nos conjuntos de resultados que ocorrem após o primeiro conjunto de resultados dependendo do tipo de gerenciador de conexões usado:  
  
-   Quando você usa gerenciadores de conexões OLE DB e ADO, a tarefa ignora os conjuntos de resultados que ocorrem após o primeiro conjunto de resultados. Portanto, com esses gerenciadores de conexões, a tarefa ignora um erro retornado por um comando SQL ou um procedimento armazenado quando o erro não faz parte do primeiro conjunto de resultados.  
  
-   Quando você usa gerenciadores de conexões ODBC e ADO.NET, a tarefa não ignora os conjuntos de resultados que ocorrem após o primeiro conjunto de resultados. Com esses gerenciadores de conexões, a tarefa falhará quando ocorrer um erro que não seja do primeiro conjunto de resultados.  
  
### <a name="custom-log-entries"></a>Entradas personalizadas do log  
 A tabela a seguir descreve a entrada de log personalizada da tarefa Executar SQL. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  
  
|Entrada de log|Descrição|  
|---------------|-----------------|  
|**ExecuteSQLExecutingQuery**|Fornece informações sobre as fases de execução da instrução SQL. As entradas de log são gravadas quando a tarefa adquire conexão com o banco de dados, quando a tarefa começa a preparar a instrução SQL e depois que a execução da instrução SQL é concluída. A entrada de log da fase de preparação inclui a instrução SQL usada pela tarefa.|  

