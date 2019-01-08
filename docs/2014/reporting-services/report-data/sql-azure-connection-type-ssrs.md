---
title: Tipo de conexão do SQL do Azure (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: c84def6c-e8cf-43d9-9912-098171a7ce79
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 6634e0b09d2a2ea83eb84e252867a4e93c4098f3
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53363028"
---
# <a name="sql-azure-connection-type-ssrs"></a>Tipo de conexão do SQL Azure (SSRS)
  [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssSDSfull](../../includes/sssdsfull-md.md)] é um banco de dados relacional hospedado baseado em nuvem, baseado nas tecnologias do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para incluir dados de um cubo do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] no seu relatório, é necessário ter um conjunto de dados baseado na fonte de dados do relatório do tipo [!INCLUDE[ssSDS](../../includes/sssds-md.md)]. Esse tipo de fonte de dados interna é baseado na extensão de dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] . Use esse tipo de fonte de dados para se conectar a e recuperar dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 Essa extensão de dados oferece suporte a parâmetros de vários valores, a agregações de servidor e a credenciais gerenciadas separadamente da cadeia de conexão.  
  
 [!INCLUDE[ssSDS](../../includes/sssds-md.md)] é semelhante a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em suas premissas, e a obtenção de dados do [!INCLUDE[ssSDS](../../includes/sssds-md.md)] , com poucas exceções, é idêntica à obtenção de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
> [!NOTE]  
>  Ao abrir uma conexão com um [!INCLUDE[ssSDS](../../includes/sssds-md.md)], defina o tempo limite da conexão para 30 segundos.  
  
 Para obter mais informações, consulte [Banco de dados SQL do Windows Azure no MSDN](https://go.microsoft.com/fwlink/?LinkId=206770). (em inglês)  
  
 Use as informações deste tópico para criar uma fonte de dados. Para obter instruções passo a passo, consulte [adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;construtor de relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md).  
  
##  <a name="Connection"></a> Cadeia de Conexão  
 Ao se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)], você está se conectando a um objeto de banco de dados na nuvem. Assim como nos bancos de dados no local, o banco de dados hospedado pode ter vários esquemas que tenham várias tabelas, exibições e procedimentos armazenados. Especifique o objeto de banco de dados a ser usado no designer de consulta. Se não especificar um banco de dados na cadeia de conexão, você se conectará ao banco de dados padrão atribuído pelo administrador.  
  
 Contate o administrador do banco de dados para obter informações sobre a conexão e as credenciais que devem ser usadas para se conectar à fonte de dados. O exemplo de cadeia de conexão a seguir especifica um banco de dados hospedado de exemplo chamado AdventureWorks.  
  
```  
Data Source=<host>;Initial Catalog=AdventureWorks; Encrypt=True;  
```  
  
 Além disso, você usa a caixa de diálogo **Propriedades de Fontes de dados** para fornecer credenciais como nome de usuário e senha. As opções `User Id` e `Password` são adicionadas automaticamente à cadeia de conexão; você não precisa digitá-las como parte da cadeia de conexão.  
  
 Para obter mais informações e exemplos de cadeias de conexão, consulte [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md).  
  
##  <a name="Credentials"></a> Credenciais  
 Não há suporte para a Autenticação do Windows (segurança integrada). Se você tentar se conectar ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] usando a Autenticação do Windows, ocorrerá um erro. [!INCLUDE[ssSDS](../../includes/sssds-md.md)] só dá suporte à Autenticação do SQL Server (nome de usuário e senha), e os usuários devem fornecer credenciais (logon e senha) toda vez que se conectam ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)].  
  
 As credenciais devem ser suficientes para acessar o banco de dados. Dependendo da consulta, você talvez precise de outras permissões, como permissões suficientes para executar procedimentos armazenados e acessar tabelas e exibições. O proprietário da fonte de dados externa deve configurar credenciais que sejam suficientes para fornecer acesso somente leitura aos objetos de banco de dados de que você precisa.  
  
 Em um cliente de criação de relatório, as seguintes opções estão disponíveis para especificar credenciais:  
  
-   Usar um nome de usuário e senha armazenados. Para negociar o salto duplo que ocorre quando o banco de dados que contém os dados de relatório é diferente do servidor de relatório, selecione as opções para usar as credenciais como credenciais do Windows. Também é possível optar por representar o usuário autenticado depois de se conectar à fonte de dados.  
  
-   Nenhuma credencial é necessária. Para usar essa opção, você deve ter a conta de execução autônoma configurada no servidor de relatório. Para obter mais informações, consulte [Configurar a conta de execução autônoma &#40;Gerenciador de Configurações do SSRS&#41;](../install-windows/configure-the-unattended-execution-account-ssrs-configuration-manager.md) na [documentação do Reporting Services](https://go.microsoft.com/fwlink/?linkid=121312) em msdn.microsoft.com.  
  
 Para obter mais informações, consulte [conexões de dados, fontes de dados e cadeias de caracteres de Conexão no Reporting Services](../data-connections-data-sources-and-connection-strings-in-reporting-services.md) ou [especificar as credenciais no construtor de relatórios](../specify-credentials-in-report-builder.md).  
  
 
  
##  <a name="Query"></a> Consultas  
 Uma consulta especifica os dados a serem recuperados de um conjunto de dados de relatório. As colunas no conjunto de resultados para uma consulta populam a coleção de campos para um conjunto de dados. Se a consulta retornar vários conjuntos de resultados, o relatório só processará o primeiro conjunto de resultados recuperado por uma consulta. Embora haja algumas diferenças entre os [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e [!INCLUDE[ssSDS](../../includes/sssds-md.md)]como os tamanhos de bancos de dados têm suporte, escrever consultas nos [!INCLUDE[ssSDS](../../includes/sssds-md.md)]é o mesmo que escrever consultas nos bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Não são suportadas algumas instruções [!INCLUDE[tsql](../../includes/tsql-md.md)] como BACKUP no [!INCLUDE[ssSDS](../../includes/sssds-md.md)], mas elas não são as que você usa nas consultas de relatório. Para obter mais informações, consulte [Tipo de conexão do SQL Server &#40;SSRS&#41;](sql-server-connection-type-ssrs.md).  
  
 Por padrão, se você criar uma nova consulta ou abrir uma consulta existente que possa ser representada no designer de consultas gráficas, o designer de consultas relacionais estará disponível. Você pode especificar uma consulta das seguintes formas:  
  
-   Crie uma consulta interativamente. Use o designer de consultas relacionais, que mostra uma exibição hierárquica de tabelas, exibições, procedimentos armazenados e outros itens de banco de dados, organizado por esquema de banco de dados. Selecione colunas em tabelas ou exibições, ou especifique procedimentos armazenados ou funções de valor de tabela. Limite o número de linhas de dados a serem recuperadas especificando critérios de filtragem. Personalize o filtro quando o relatório for executado definindo a opção de parâmetro.  
  
-   Digite ou cole uma consulta. Use o designer de consulta baseado em texto para inserir o texto do [!INCLUDE[tsql](../../includes/tsql-md.md)] diretamente, colar texto de consulta de outra fonte, inserir consultas complexas que não podem ser criadas com o designer de consultas relacionais ou inserir expressões baseadas em consulta.  
  
-   Importa uma consulta existente de um arquivo ou relatório. Use o botão **Importar** consulta em qualquer designer de consulta para navegar até um arquivo .sql ou .rdl e importar uma consulta.  
  
 O designer de consultas com base em texto oferece aos dois modos a seguir:  
  
-   [Texto](#QueryText) Digite os comandos do [!INCLUDE[tsql](../../includes/tsql-md.md)] que selecionam dados da fonte de dados.  
  
-   [Procedimento armazenado](#QueryStoredProcedure) Escolha em uma lista de procedimentos armazenados.  
  
 Para obter mais informações, consulte [Interface do usuário do Designer de Consultas Relacionais &#40;Construtor de Relatórios&#41;](relational-query-designer-user-interface-report-builder.md) e [Interface do usuário do Designer de Consultas Baseadas em Texto &#40;Construtor de Relatórios&#41;](text-based-query-designer-user-interface-report-builder.md).  
  
 O designer de consultas gráficas usado pelo [!INCLUDE[ssSDS](../../includes/sssds-md.md)] fornece suporte interno ao agrupamento e às agregações para ajudar a escrever consultas que só recuperam dados resumidos. Os recursos de linguagem do [!INCLUDE[tsql](../../includes/tsql-md.md)] são: a cláusula GROUP BY, a palavra-chave DISTINCT e agregações, como SUM e COUNT. O designer de consultas baseado em texto dá suporte completo para a linguagem do [!INCLUDE[tsql](../../includes/tsql-md.md)] , incluindo agrupamentos e agregações. Para obter mais informações sobre o [!INCLUDE[tsql](../../includes/tsql-md.md)], consulte [Referência do Transact-SQL &#40;Mecanismo de Banco de Dados&#41;](/sql/t-sql/language-reference)nos [Manuais Online](https://go.microsoft.com/fwlink/?LinkId=141687) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em msdn.microsoft.com.  
  
###  <a name="QueryText"></a> Usando o tipo de consulta Text  
 No designer de consulta baseado em texto, você digita os comandos do [!INCLUDE[tsql](../../includes/tsql-md.md)] para definir os dados em um conjunto de dados. Por exemplo, a seguinte consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] seleciona os nomes de todos os funcionários que são assistentes de marketing:  
  
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
  
```  
WHERE HumanResources.Employee.JobTitle = (@JobTitle)  
```  
  
 Quando você executa a consulta, os parâmetros do relatório que correspondem aos parâmetros da consulta serão criados automaticamente. Para obter mais informações, consulte [Parâmetros de consulta](#Parameters) mais adiante neste tópico.  
  
  
  
###  <a name="QueryStoredProcedure"></a> Usando o tipo de consulta StoredProcedure  
 Você pode especificar um procedimento armazenado para uma consulta de conjunto de dados das seguintes maneiras:  
  
-   Na caixa de diálogo **Propriedades do Conjunto de dados** , defina a opção **Procedimento Armazenado** . Faça suas escolhas na lista suspensa de procedimentos armazenados e funções avaliadas por tabela.  
  
-   No designer de consulta relacional, no painel de exibição Banco de Dados, selecione um procedimento armazenado ou função avaliada por tabela.  
  
-   No designer de consulta baseado em texto, selecione **StoredProcedure** na barra de ferramentas.  
  
 Após selecionar um procedimento armazenado ou função avaliada por tabela, você pode executar a consulta. Você receberá uma solicitação para obter valores de parâmetro de entrada. Quando você executa a consulta, os parâmetros do relatório que correspondem aos parâmetros de entrada serão criados automaticamente. Para obter mais informações, consulte [Parâmetros de consulta](#Parameters) mais adiante neste tópico.  
  
 Somente o primeiro conjunto de resultados recuperado para um procedimento armazenado é suportado. Se um procedimento armazenado retornar vários conjuntos de resultados, somente o primeiro será usado.  
  
 Se um procedimento armazenado tiver um parâmetro com um valor padrão, você poderá acessar esse valor usando a palavra-chave DEFAULT como valor para o parâmetro. Se o parâmetro de consulta estiver vinculado a um parâmetro de relatório, o usuário poderá digitar ou selecionar a palavra DEFAULT na caixa de entrada do parâmetro de relatório.  
  
 Para obter mais informações sobre procedimentos armazenados, consulte "Procedimentos armazenados (mecanismo de banco de dados)" nos [Manuais Online do SQL Server](https://go.microsoft.com/fwlink/?linkid=98335) em msdn.microsoft.com.  
  
  
  
##  <a name="Parameters"></a> Parâmetros  
 Quando o texto de consulta contém variáveis ou procedimentos armazenados com parâmetros de entrada, os parâmetros de consulta para o conjunto de dados e os parâmetros de relatório para o relatório são automaticamente gerados. O texto de consulta não deve incluir uma instrução DECLARE para cada variável de consulta.  
  
 Por exemplo, a consulta SQL a seguir cria um parâmetro de relatório chamado `EmpID`:  
  
```  
SELECT FirstName, LastName FROM HumanResources.Employee E INNER JOIN  
       Person.Contact C ON  E.ContactID=C.ContactID   
WHERE EmployeeID = (@EmpID)  
```  
  
 Por padrão, cada parâmetro de relatório tem o tipo de dados Texto e um conjunto de dados criado automaticamente para fornecer uma lista suspensa dos valores disponíveis. Depois que os parâmetros de relatório forem criados, talvez seja necessário alterar os valores padrão. Para obter mais informações, consulte [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md).  
  
  
  
##  <a name="Remarks"></a> Comentários  
  
###### <a name="alternate-data-extensions"></a>Extensões de dados alternativas  
 Também é possível recuperar dados de um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um tipo de fonte de dados ODBC. Não há suporte para a conexão ao [!INCLUDE[ssSDS](../../includes/sssds-md.md)] com o uso do OLE DB.  
  
 Para obter mais informações, consulte [Tipo de conexão ODBC &#40;SSRS&#41;](odbc-connection-type-ssrs.md).  
  
###### <a name="platform-and-version-information"></a>Informações sobre plataforma e versão  
 Para obter mais informações sobre o suporte de plataforma e à versão, consulte [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
  
  
##  <a name="HowTo"></a> Tópicos de instruções  
 Esta seção contém instruções passo a passo para trabalhar com conexões de dados, fontes de dados e conjuntos de dados.  
  
 [Adicionar e verificar uma Conexão de dados ou uma fonte de dados &#40;relatórios e SSRS&#41;](add-and-verify-a-data-connection-report-builder-and-ssrs.md)  
  
 [Criar um conjunto de dados compartilhado ou um conjunto de dados inserido &#40;Construtor de Relatórios e SSRS&#41;](create-a-shared-dataset-or-embedded-dataset-report-builder-and-ssrs.md)  
  
 [Adicionar um filtro a um conjunto de dados &#40;Construtor de Relatórios e SSRS&#41;](add-a-filter-to-a-dataset-report-builder-and-ssrs.md)  
  
  
  
##  <a name="Related"></a> Seções relacionadas  
 Estas seções da documentação especificam informações conceituais detalhadas sobre os dados do relatório e informações de procedimentos sobre como definir, personalizar e usar partes de um relatório relacionadas aos dados.  
  
 [Adicionar dados a um relatório &#40;relatórios e SSRS&#41;](report-datasets-ssrs.md)  
 Fornece uma visão geral de como acessar dados de seu relatório.  
  
 [Conexões de dados, fontes de dados e cadeias de conexão no Construtor de Relatórios](../data-connections-data-sources-and-connection-strings-in-report-builder.md)  
 Fornece informações sobre conexões de dados e fontes de dados.  
  
 [Conjuntos de dados inseridos e compartilhados de relatório &#40;Construtor de Relatórios e SSRS&#41;](report-embedded-datasets-and-shared-datasets-report-builder-and-ssrs.md)  
 Fornece informações sobre conjuntos de dados inseridos e compartilhados.  
  
 [Coleção de campos de conjuntos de dados &#40;Construtor de Relatórios e SSRS&#41;](dataset-fields-collection-report-builder-and-ssrs.md)  
 Fornece informações sobre a coleção de campos de conjuntos de dados gerada pela consulta.  
  
 [Fontes de dados com suporte no Reporting Services &#40;SSRS&#41;](../create-deploy-and-manage-mobile-and-paginated-reports.md) na documentação do [!INCLUDE[ssRSnoversion](../../../includes/ssrsnoversion-md.md)] nos [Manuais Online](https://go.microsoft.com/fwlink/?linkid=121312) do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
 Fornece informações detalhadas sobre suporte à plataforma e à versão para cada extensão de dados.  
  
  
  
## <a name="see-also"></a>Consulte também  
 [Parâmetros de relatório &#40;Construtor de Relatórios e Designer de Relatórios&#41;](../report-design/report-parameters-report-builder-and-report-designer.md)   
 [Filtrar, agrupar e classificar dados &#40;Construtor de Relatórios e SSRS&#41;](../report-design/filter-group-and-sort-data-report-builder-and-ssrs.md)   
 [Expressões &#40;Construtor de Relatórios e SSRS&#41;](../report-design/expressions-report-builder-and-ssrs.md)  
  
  
