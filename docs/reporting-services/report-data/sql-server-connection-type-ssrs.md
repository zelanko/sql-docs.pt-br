---
title: Tipo de conexão do SQL Server (SSRS) | Microsoft Docs
ms.date: 08/17/2018
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: report-data
ms.topic: conceptual
ms.assetid: 957e7091-e08f-48d2-9506-872227ae8b20
author: markingmyname
ms.author: maghan
ms.openlocfilehash: f96aaf47e728119b20e3fcdee0709115e30bc40b
ms.sourcegitcommit: 61381ef939415fe019285def9450d7583df1fed0
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/01/2018
ms.locfileid: "47611935"
---
# <a name="sql-server-connection-type-ssrs"></a>O tipo de conexão do SQL Server (SSRS)
  Para incluir dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Esse tipo de fonte de dados interna é baseado na extensão de dados do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Use esse tipo de fonte de dados para se conectar e para recuperar dados de uma versão atual e de versões anteriores de bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Essa extensão de dados dá suporte a parâmetros de vários valores, a agregações de servidor e a credenciais gerenciadas separadamente da cadeia de conexão.  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [Adicionar e verificar uma conexão de dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Ao se conectar a um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , você está se conectando ao objeto de banco de dados em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um servidor. O banco de dados pode ter vários esquemas que tenham várias tabelas, exibições e procedimentos armazenados. Especifique o objeto de banco de dados a ser usado no designer de consulta. Se não especificar um banco de dados na cadeia de conexão, você será conectado ao banco de dados padrão atribuído pelo administrador do banco de dados.  
  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica um banco de dados de exemplo no cliente local:  
  
```  
Data Source=<server>;Initial Catalog=AdventureWorks  
```  
  
 Para obter mais informações sobre exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](http://msdn.microsoft.com/library/7e103637-4371-43d7-821c-d269c2cc1b34).  
  
##  <a name="Credentials"></a> Credenciais  
 As credenciais são necessárias para executar consultas, visualizar o relatório localmente e visualizá-lo no servidor de relatório.  
  
 Após a publicação do relatório, talvez seja necessário alterar as credenciais da fonte de dados para que, quando o relatório for executado no servidor de relatório, as permissões recuperadas sejam válidas.  
  
 Em um cliente de criação de relatório, as seguintes opções estão disponíveis para especificar credenciais:  
  
-   Usuário atual do Windows (também conhecido como segurança integrada).  
  
-   Usar um nome de usuário e senha armazenados.  
  
-   Solicitar credenciais ao usuário. Essa opção só dá suporte à segurança integrada do Windows.  
  
-   Nenhuma credencial é necessária. Para usar essa opção, você deve ter a conta de execução autônoma configurada no servidor de relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../../reporting-services/install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na [documentação do Reporting Services](http://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
 Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md) ou [Especificar as credenciais no Construtor de Relatórios](http://msdn.microsoft.com/library/7412ce68-aece-41c0-8c37-76a0e54b6b53).  
  
  
##  <a name="Query"></a> Consultas  
 Uma consulta especifica os dados a serem recuperados de um conjunto de dados de relatório. As colunas no conjunto de resultados para uma consulta populam a coleção de campos para um conjunto de dados. Um relatório só processa o primeiro conjunto de resultados recuperado por uma consulta.  
  
 Por padrão, se você criar uma nova consulta ou abrir uma consulta existente que possa ser representada no designer de consultas gráficas, o designer de consultas relacionais estará disponível. Você pode especificar uma consulta das seguintes formas:  
  
-   Crie uma consulta interativamente. Use o designer de consultas relacionais, que mostra uma exibição hierárquica de tabelas, exibições, procedimentos armazenados e outros itens de banco de dados, organizado por esquema de banco de dados. Selecione colunas em tabelas ou exibições, ou especifique procedimentos armazenados ou funções de valor de tabela. Limite o número de linhas de dados a serem recuperadas especificando critérios de filtragem. Personalize o filtro quando o relatório for executado definindo a opção de parâmetro.  
  
-   Digite ou cole uma consulta. Use o designer de consulta baseado em texto para inserir o texto do [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente, colar texto de consulta de outra fonte, inserir consultas complexas que não podem ser criadas com o designer de consultas relacionais ou inserir expressões baseadas em consulta.  
  
-   Importa uma consulta existente de um arquivo ou relatório. Use o botão **Importar** consulta em qualquer designer de consulta para navegar até um arquivo .sql ou .rdl e importar uma consulta.  
  
 Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Relacionais &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/relational-query-designer-user-interface-report-builder.md) e [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](../../reporting-services/report-data/text-based-query-designer-user-interface-report-builder.md).  
  
 Há suporte para os seguintes modos de consulta:  
  
-   Tipo[Text](#QueryText) nos comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] .  
  
-   [Procedimento armazenado](#QueryStoredProcedure) Escolha em uma lista de procedimentos armazenados.  
  
###  <a name="QueryText"></a> Usando o tipo de consulta Text  
 No designer de consulta baseado em texto, você pode digitar os comandos [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir os dados em um conjunto de dados. Por exemplo, a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona os nomes de todos os funcionários que são assistentes de marketing:  
  
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
  
  
###  <a name="QueryStoredProcedure"></a> Usando o tipo de consulta StoredProcedure  
 Você pode especificar um procedimento armazenado para uma consulta de conjunto de dados das seguintes maneiras:  
  
-   Na caixa de diálogo **Propriedades do Conjunto de dados** , defina a opção **Procedimento Armazenado** . Faça suas escolhas na lista suspensa de procedimentos armazenados e funções avaliadas por tabela.  
  
-   No designer de consulta relacional, no painel de exibição Banco de Dados, selecione um procedimento armazenado ou função avaliada por tabela.  
  
-   No designer de consulta baseado em texto, selecione **StoredProcedure** na barra de ferramentas.  
  
 Após selecionar um procedimento armazenado ou função avaliada por tabela, você pode executar a consulta. Você receberá uma solicitação para obter valores de parâmetro de entrada. Quando você executa a consulta, os parâmetros do relatório que correspondem aos parâmetros de entrada serão criados automaticamente. Para obter mais informações, consulte [Parâmetros de consulta](#Parameters) mais adiante neste tópico.  
  
 Somente o primeiro conjunto de resultados recuperado para um procedimento armazenado é suportado. Se um procedimento armazenado retornar vários conjuntos de resultados, somente o primeiro será usado.  
  
 Se um procedimento armazenado tiver um parâmetro com um valor padrão, você poderá acessar esse valor usando a palavra-chave DEFAULT como valor para o parâmetro. Se o parâmetro de consulta estiver vinculado a um parâmetro de relatório, o usuário poderá digitar ou selecionar a palavra DEFAULT na caixa de entrada do parâmetro de relatório.  
  
 Para obter mais informações, consulte [Criar procedimentos armazenados (Mecanismo de Banco de Dados](../../relational-databases/stored-procedures/stored-procedures-database-engine.md)).  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Quando o texto de consulta contém variáveis ou procedimentos armazenados com parâmetros de entrada, os parâmetros de consulta para o conjunto de dados e os parâmetros de relatório para o relatório são automaticamente gerados. O texto de consulta não deve incluir uma instrução DECLARE para cada variável de consulta.  
  
 Por exemplo, a consulta SQL a seguir cria um parâmetro de relatório chamado **EmpID**:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 Os parâmetros de relatório são criados com valores de propriedade padrão que talvez precisem ser modificados. Por exemplo:  
  
-   Por padrão, cada parâmetro de relatório é do tipo de dados **Texto**. Se os dados subjacentes forem de outro tipo de dados, será necessário alterar o tipo de dados de parâmetro.  
  
-   Se você selecionar a opção para parâmetros de vários valores, deverá alterar manualmente a consulta para testar se os valores fazem parte de um conjunto usando o operador **IN** , por exemplo, `WHERE EmployeeID IN (@EmpID)`.  
  
 Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
##  <a name="Remarks"></a> Comentários  
 Você também pode recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com o uso de um tipo de fonte de dados do OLE DB ou ODBC. Para obter mais informações, consulte [Tipo de conexão do OLE DB &#40;SSRS&#41;](../../reporting-services/report-data/ole-db-connection-type-ssrs.md) ou [Tipo de conexão do ODBC&#40;SSRS&#41;](../../reporting-services/report-data/odbc-connection-type-ssrs.md).  
  
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
  
  
## <a name="see-also"></a>Consulte Também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../../reporting-services/report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/expressions-report-builder-and-ssrs.md)  
  
  
