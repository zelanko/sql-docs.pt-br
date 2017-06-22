---
title: "SQL Server Parallel Data Warehouse (SSRS) do tipo de Conexão | Microsoft Docs"
ms.custom: 
ms.date: 05/30/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 3925fd3d-2aa1-4768-96ad-cfc2c0ba9283
caps.latest.revision: 10
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 6b968bb97c484834915f2fdfb9b0ac294243810a
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---

# <a name="sql-server-parallel-data-warehouse-connection-type-ssrs"></a>Tipo de conexão do SQL Server Parallel Data Warehouse (SSRS)

  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] é um aplicativo de data warehouse escalonável que fornece desempenho e escalabilidade por meio de um processamento paralelo em massa. [!INCLUDE[ssDW](../../includes/ssdw-md.md)]usa bancos de dados do SQL Server para armazenamento de dados e processamento distribuído.  
  
 As tabelas de banco de dados grande de partições de dispositivo em vários nós físicos, com cada nó executando sua própria instância do SQL Server. Ao se conectar ao [!INCLUDE[ssDW](../../includes/ssdw-md.md)] para recuperar dados de relatório, um relatório se conecta ao nó de controle, que gerencia o processamento de consulta no aplicativo [!INCLUDE[ssDW](../../includes/ssdw-md.md)] . Depois que a conexão é estabelecida, não há nenhuma diferença entre trabalhar com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que esteja dentro e com uma que esteja fora de um ambiente do [!INCLUDE[ssDW](../../includes/ssdw-md.md)] .  
  
 Para incluir dados do [!INCLUDE[ssDW](../../includes/ssdw-md.md)] no relatório, você deve ter um conjunto de dados baseado em uma fonte de dados de relatório do tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Parallel Data Warehouse. Esse tipo de fonte de dados interna se baseia na extensão de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Parallel Data Warehouse. Use esse tipo de fonte de dados para se conectar a e recuperar dados do [!INCLUDE[ssDW](../../includes/ssdw-md.md)].  
  
 Essa extensão de dados oferece suporte a parâmetros de vários valores, a agregações de servidor e a credenciais gerenciadas separadamente da cadeia de conexão.  
  
 Para obter mais informações, consulte o site [SQL Server 2008 R2 Parallel Data Warehouse](http://go.microsoft.com/fwlink/?LinkId=150895).  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Ao se conectar ao [!INCLUDE[ssDW](../../includes/ssdw-md.md)], você está conectando a um objeto de banco de dados dentro de um aplicativo [!INCLUDE[ssDW](../../includes/ssdw-md.md)] . Especifique o objeto de banco de dados a ser usado no designer de consulta. Se não especificar um banco de dados na cadeia de conexão, você se conectará ao banco de dados padrão atribuído pelo administrador. Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo da cadeia de conexão a seguir especifica o banco de dados de exemplo, **CustomerSales**, no aplicativo [!INCLUDE[ssDW](../../includes/ssdw-md.md)] :  
  
```  
HOST=<IP address>; database= CustomerSales; port=<port>  
```  
  
 Além disso, você usa a caixa de diálogo **Propriedades das Fontes de Dados** para fornecer credenciais, como nome de usuário e senha. As opções `User Id` e `Password` são acrescentadas automaticamente à cadeia de conexão; você não precisa digitá-las como parte da cadeia de conexão. A interface de usuário também fornece opções para especificar o endereço IP do nó de controle no aplicativo [!INCLUDE[ssDW](../../includes/ssdw-md.md)] e o número da porta. Por padrão, a porta é a 17000. A porta é configurável por um administrador, e a cadeia de conexão talvez use um número de porta diferente.  
  
 Para obter mais informações sobre exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
##  <a name="Credentials"></a> Credenciais  
 [!INCLUDE[ssDW](../../includes/ssdw-md.md)] fornece sua própria tecnologia de segurança para implementar e armazenar nomes de usuários e senhas. Não é possível usar a Autenticação do Windows. Se você tentar se conectar ao [!INCLUDE[ssDW](../../includes/ssdw-md.md)] usando a Autenticação do Windows, ocorrerá um erro.  
  
 As credenciais devem ser suficientes para acessar o banco de dados. Dependendo da consulta, você talvez precise de outras permissões, como permissões suficientes para acessar tabelas e exibições. O proprietário da fonte de dados externa deve configurar credenciais que sejam suficientes para fornecer acesso somente leitura aos objetos de banco de dados de que você precisa.  
  
 Em um cliente de criação de relatório, as seguintes opções estão disponíveis para especificar credenciais:  
  
-   Usar um nome de usuário e senha armazenados. Para negociar o salto duplo que ocorre quando o banco de dados que contém os dados de relatório é diferente do servidor de relatório, selecione as opções para usar as credenciais como credenciais do Windows. Também é possível optar por representar o usuário autenticado depois de se conectar à fonte de dados.  
  
-   Nenhuma credencial é necessária. Para usar essa opção, você deve ter a conta de execução autônoma configurada no servidor de relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na [documentação do Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Uma consulta especifica os dados a serem recuperados de um conjunto de dados de relatório.  
  
 As colunas no conjunto de resultados para uma consulta populam a coleção de campos para um conjunto de dados. Se a consulta retornar vários conjuntos de resultados, o relatório só processará o primeiro conjunto de resultados recuperado por uma consulta. Por padrão, se você criar uma nova consulta ou abrir uma consulta existente que possa ser representada no designer de consultas gráficas, o designer de consultas relacionais estará disponível. Você pode especificar uma consulta das seguintes formas:  
  
-   Crie uma consulta interativamente. Use o designer de consulta relacional que mostra uma exibição hierárquica de tabelas, exibições e outros itens de banco de dados, organizado por esquema de banco de dados. Selecione colunas de tabelas ou exibições. Limite o número de linhas de dados a serem recuperadas especificando critérios de filtragem, agrupamentos e agregações. Personalize o filtro quando o relatório for executado definindo a opção de parâmetro.  
  
-   Digite ou cole uma consulta. Use o designer de consulta baseado em texto para inserir o texto do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] diretamente, colar texto de consulta de outra fonte, inserir consultas complexas que não podem ser criadas com o designer de consultas relacionais ou inserir expressões baseadas em consulta.  
  
-   Importa uma consulta existente de um arquivo ou relatório. Use o botão **Importar** consulta em qualquer designer de consulta para navegar até um arquivo .sql ou .rdl e importar uma consulta.  
  
 Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Relacionais &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md) e [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 O designer de consultas baseadas em texto dá suporte ao modo de [Texto](#QueryText) no qual você digita comandos [!INCLUDE[DWsql](../../includes/dwsql-md.md)] que selecionam dados da fonte de dados.  
  
-   [Texto](#QueryText)  
  
 Você usa [!INCLUDE[DWsql](../../includes/dwsql-md.md)] com [!INCLUDE[ssDW](../../includes/ssdw-md.md)] e [!INCLUDE[tsql](../../includes/tsql-md.md)] com o SQL Server. Os dois dialetos da linguagem SQL são bem semelhantes. As consultas escritas para o tipo de conexão da fonte de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] normalmente podem ser usadas para o tipo de conexão da fonte de dados do [!INCLUDE[ssDWCurrentFull](../../includes/ssdwcurrentfull-md.md)] .  
  
 Uma consulta que recupera dados de relatório de um banco de dados grande, inclusive um data warehouse como [!INCLUDE[ssDW](../../includes/ssdw-md.md)]pode gerar um conjunto de resultados com um número muito grande de linhas, a menos que você agregue e resuma dados para reduzir o número de linhas retornados pela consulta. É possível escrever consultas que incluam agregações e agrupamentos usando o designer de consultas gráficas ou baseado em texto.  
  
 [!INCLUDE[DWsql](../../includes/dwsql-md.md)] dá suporte à cláusula, à palavra-chave e às agregações fornecidas pelo designer de consulta para resumir dados.  
  
 O designer de consultas gráficas usado pelo [!INCLUDE[ssDW](../../includes/ssdw-md.md)] fornece suporte interno ao agrupamento e às agregações para ajudar a escrever consultas que recuperam apenas dados de resumo. Os recursos de linguagem do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] são: a cláusula GROUP BY, a palavra-chave DISTINCT e agregações, como SUM e COUNT. O designer de consultas baseado em texto dá suporte completo para a linguagem do [!INCLUDE[DWsql](../../includes/dwsql-md.md)], incluindo agrupamentos e agregações.  
  
 Para obter mais informações sobre o [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](../../t-sql/transact-sql-reference-database-engine.md)nos [Manuais Online](http://go.microsoft.com/fwlink/?LinkId=141687) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
###  <a name="QueryText"></a> Usando o tipo de consulta Text  
 No designer de consulta baseado em texto, você digita os comandos do [!INCLUDE[DWsql](../../includes/dwsql-md.md)] para definir os dados em um conjunto de dados. As consultas que você usa para recuperar dados do [!INCLUDE[ssDW](../../includes/ssdw-md.md)] são as mesmas usadas para recuperar dados de instâncias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que não estejam em execução dentro de um aplicativo do [!INCLUDE[ssDW](../../includes/ssdw-md.md)] . Por exemplo, a seguinte consulta [!INCLUDE[DWsql](../../includes/dwsql-md.md)] seleciona os nomes de todos os funcionários que são assistentes de marketing:  
  
```  
SELECT  
  HumanResources.Employee.BusinessEntityID  
  ,HumanResources.Employee.JobTitle  
  ,Person.Person.FirstName  
  ,Person.Person.LastName  
FROM  
  Person.Person  
  INNER JOIN HumanResources.Employee  
    ON Person.Person.BusinessEntityID = HumanResources.Employee.BusinessEntityID  
WHERE HumanResources.Employee.JobTitle = 'Marketing Assistant'   
```  
  
 Clique no botão **Executar** (**!**) na barra de ferramentas para executar a consulta e exibir um conjunto de resultados.  
  
 Para parametrizar essa consulta, adicione um parâmetro de consulta. Por exemplo, altere a cláusula WHERE para o seguinte:  
  
 `WHERE HumanResources.Employee.JobTitle = (@JobTitle)`  
  
 Quando você executa a consulta, os parâmetros do relatório que correspondem aos parâmetros da consulta serão criados automaticamente. Para obter mais informações, consulte [Parâmetros de consulta](#Parameters) mais adiante neste tópico.  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Quando o texto de consulta contém variáveis ou procedimentos armazenados com parâmetros de entrada, os parâmetros de consulta para o conjunto de dados e os parâmetros de relatório para o relatório são automaticamente gerados. O texto de consulta não deve incluir uma instrução DECLARE para cada variável de consulta.  
  
 Por exemplo, a consulta SQL a seguir cria um parâmetro de relatório chamado **EmpID**:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 Por padrão, cada parâmetro de relatório tem o tipo de dados Texto e um conjunto de dados criado automaticamente para fornecer uma lista suspensa dos valores disponíveis. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentários  
  
###### <a name="platform-and-version-information"></a>Informações sobre plataforma e versão  
 Para obter mais informações sobre o suporte de plataforma e à versão, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação especificam informações conceituais detalhadas sobre os dados do relatório e informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Conjuntos de dados de relatório &#40;SSRS&#41;](../../reporting-services/report-data/report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../../reporting-services/report-data/data-sources-supported-by-reporting-services-ssrs.md) na documentação do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] nos [Manuais Online](http://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  

## <a name="next-steps"></a>Próximas etapas

[Parâmetros de relatório](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
[Filtrar, agrupar e classificar dados](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
[Expressões](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  

Mais perguntas? [Tente fazer o fórum do Reporting Services](http://go.microsoft.com/fwlink/?LinkId=620231)
