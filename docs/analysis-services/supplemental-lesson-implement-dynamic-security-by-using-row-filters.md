---
title: "Implementar a segurança dinâmica usando filtros de linha | Microsoft Docs"
ms.custom: 
ms.date: 04/10/2017
ms.prod: 
ms.reviewer: 
ms.suite: 
ms.technology:
- analysis-services
ms.tgt_pltfrm: 
ms.topic: get-started-article
applies_to: 
ms.assetid: 
author: Minewiskan
ms.author: owend
manager: erikre
ms.translationtype: MT
ms.sourcegitcommit: 876522142756bca05416a1afff3cf10467f4c7f1
ms.openlocfilehash: 14bc3755dcbb92af2f75ed47a4df6843fe4782b4
ms.contentlocale: pt-br
ms.lasthandoff: 09/01/2017

---
# <a name="supplemental-lesson---implement-dynamic-security-by-using-row-filters"></a>Lição suplementar - implementar a segurança dinâmica usando filtros de linha
[!INCLUDE[ssas-appliesto-sql2016-later-aas](../includes/ssas-appliesto-sql2016-later-aas.md)]

Nesta lição suplementar, você criará uma função adicional que implementa a segurança dinâmica. A segurança dinâmica oferece segurança em nível de linha com base no nome de usuário ou na id de logon do usuário conectado no momento. Para obter mais informações, consulte [Funções](../analysis-services/tabular-models/roles-ssas-tabular.md).  
  
Para implementar a segurança dinâmica, você deverá adicionar uma tabela a seu modelo contendo os nomes de usuários Windows desses usuários que podem criar uma conexão com o modelo como uma fonte de dados e procurar objetos e dados do modelo. O modelo criado usando este tutorial está no contexto da Adventure Works Corp.; entretanto, para concluir esta lição, você deve adicionar uma tabela contendo os usuários de seu próprio domínio. Você não precisará das senhas para os nomes de usuários que serão adicionados. Para criar uma tabela de EmployeeSecurity, com uma pequena amostra dos usuários de seu próprio domínio, você usará o recurso Colar, colando dados de funcionários de uma planilha do Excel. Em um cenário do mundo real, a tabela que contém nomes de usuários adicionada a um modelo normalmente empregaria uma tabela de um banco de dados real como uma fonte de dados; por exemplo, uma tabela real dimEmployee.  
  
Para implementar a segurança dinâmica, você usará duas novas funções DAX: [Função USERNAME (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f) e [Função LOOKUPVALUE (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab). Estas funções, aplicadas em um fórmula de filtro de linha, são definidas em uma nova função. Usando a função LOOKUPVALUE, a fórmula Especifica um valor da tabela EmployeeSecurity e, em seguida, passa a que o valor para a função de nome de usuário, que especifica o nome de usuário do usuário conectado pertence a essa função. O usuário pode procurar apenas nos dados especificados pelos filtros de linha da função. Neste cenário, você especificará que os funcionários de vendas só podem procurar dados de vendas pela internet para as regiões de vendas das quais eles são membro.  
  
Para concluir esta lição suplementar, você executará uma série de tarefas. Essas tarefas que são exclusivas deste cenário de modelo de tabela do Adventure Works, mas não se aplicariam necessariamente a um cenário do mundo real, são identificadas como tal. Cada tarefa inclui informações adicionais que descrevem o propósito da tarefa.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
Este tópico complementar da lição faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição suplementar, conclua todas as lições anteriores.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Adicione a tabela dimSalesTerritory ao Projeto de Modelo de Tabela de Vendas pela Internet da AW  
Para implementar a segurança dinâmica para este cenário do Adventure Works, inclua duas tabelas adicionais no seu modelo. A primeira tabela que você adicionará é dimSalesTerritory (como Sales Territory) do mesmo banco de dados AdventureWorksDW. Posteriormente, você aplicará um filtro de linha à tabela SalesTerritory que define os dados específicos que do usuário conectado pode procurar.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Para adicionar a tabela dimSalesTerritory  
  
1.  No SSDT, clique no **modelo** menu e clique **conexões existentes**.  
  
2.  Na caixa de diálogo **Conexões Existentes** , verifique se a conexão da fonte de dados **Adventure Works DB do SQL** está selecionada e clique em **Abrir**.  
  
    Se a caixa de diálogo Credenciais de Representação aparecer, digite as credenciais de representação usadas na Lição 2: Adicionar dados.  
  
3.  Na página **Escolher Como Importar os Dados** , deixe marcada a opção **Selecionar itens em uma lista de tabelas e exibições para escolher os dados a serem importados** e clique em **Avançar**.  
  
4.  Na página **Selecionar Tabelas e Exibições** , selecione a tabela **DimSalesTerritory** .  
  
5.  Clique em **Visualizar e Filtrar**.  
  
6.  Desmarque a coluna **SalesTerritoryAlternateKey** e clique em **OK**.  
  
7.  Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
    A nova tabela será adicionada ao espaço de trabalho do modelo. Objetos e dados da tabela de origem DimSalesTerritory, em seguida, são importados para o modelo de tabela de vendas de Internet AW.  
  
9. Depois que a tabela for importada, clique em **Fechar**.  

## <a name="add-a-table-with-user-name-data"></a>Adicione uma tabela com dados de nome de usuário  
Como a tabela dimEmployee no banco de dados de exemplo AdventureWorksDW contém usuários do domínio AdventureWorks, e esses nomes de usuários não existem em seu próprio ambiente, crie uma tabela em seu modelo que contenha um exemplo pequeno (três) de usuários reais de sua organização. Você adicionará estes usuários como membros à nova função. Você não precisa das senhas para os nomes de usuários de exemplo, mas precisará dos nomes de usuários reais do Windows de seu próprio domínio.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Para adicionar uma tabela EmployeeSecurity  
  
1.  Abra o Microsoft Excel, criando uma nova planilha.  
  
2.  Copie a tabela a seguir, inclusive a linha de cabeçalho, e cole-a na planilha.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Substitua o nome, sobrenome e domínio ome de usuário com os nomes e ids de logon de três usuários em sua organização. Coloque o mesmo usuário nas duas primeiras linhas, para 1 EmployeeId. Isso mostrará que este usuário pertence a mais de uma região de vendas. Deixe os campos EmployeeId e SalesTerritoryId como estão.  
  
4.  Salve a planilha como **SampleEmployee**.  
  
5.  Na planilha, selecione todas as células com dados de funcionário, inclusive os cabeçalhos, em seguida, clique os dados selecionados e, em seguida, clique em **cópia**.  
  
6.  No SSDT, clique no **editar** menu e clique **colar**.  
  
    Se colar estiver esmaecido, clique em qualquer coluna em qualquer tabela na janela do designer de modelo e tente novamente.  
  
7.  No **visualização de colagem** na caixa **nome de tabela**, tipo **EmployeeSecurity**.  
  
8.  Em **dados a serem colados**, verifique se os dados incluem todos os dados de usuário e os cabeçalhos da planilha SampleEmployee.  
  
9. Verifique se a opção **Usar a primeira linha como cabeçalhos de coluna** está marcada e clique em **OK**.  
  
    Uma nova tabela denominada EmployeeSecurity com dados de funcionário copiados da planilha SampleEmployee é criada.  
  
## <a name="create-relationships-between-factinternetsales-dimgeography-and-dimsalesterritory-table"></a>Criar relações entre tabelas FactInternetSales, DimGeography e DimSalesTerritory  
A tabela FactInternetSales, DimGeography e DimSalesTerritory contém uma coluna comum, SalesTerritoryId. A coluna SalesTerritoryId na tabela DimSalesTerritory contém valores com uma Id diferente para cada região de vendas.  
  
#### <a name="to-create-relationships-between-the-factinternetsales-dimgeography-and-the-dimsalesterritory-table"></a>Para criar relações entre o FactInternetSales, DimGeography e a tabela DimSalesTerritory  
  
1.  No designer de modelo, na exibição de diagrama no **DimGeography** de tabela, clique e mantenha o **SalesTerritoryId** coluna, em seguida, arraste o cursor para o **SalesTerritoryId** coluna de **DimSalesTerritory** de tabela e, em seguida, solte.  
  
2.  No **FactInternetSales** de tabela, clique e mantenha o **SalesTerritoryId** coluna, em seguida, arraste o cursor para o **SalesTerritoryId** coluna no  **DimSalesTerritory** da tabela e, em seguida, solte.  
  
    Observe que a propriedade ativa desta relação é False, o que significa que ele está inativo. Isso ocorre porque a tabela FactInternetSales já tem outra relação ativa que é usada em medidas.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Ocultar a tabela de EmployeeSecurity de aplicativos cliente  
Nesta tarefa, você ocultará a tabela de EmployeeSecurity, impedindo que ela apareça na lista de campos de um aplicativo cliente. Lembre-se de que, ao ocultar uma tabela, você não a protege. Os usuários podem consultar os dados da tabela EmployeeSecurity ainda se souberem como. Para proteger os dados da tabela EmployeeSecurity, impedindo que os usuários possam consultar seus dados, você aplicará um filtro em uma tarefa posterior.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>Para ocultar a tabela de EmployeeSecurity de aplicativos cliente  
  
-   No designer de modelos, em Exibição de Diagrama, clique com o botão direito do mouse no cabeçalho da tabela **Funcionário** e clique em **Ocultar das Ferramentas de Cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Criar uma função de usuário Sales Employees by Territory  
Nesta tarefa, você criará uma nova função de usuário. Esta função incluirá um filtro de linha que define quais linhas da tabela DimSalesTerritory são visíveis aos usuários. O filtro é aplicado, em seguida, na direção para todas as outras tabelas relacionadas à DimSalesTerritory relação um-para-muitos. Você também aplicará um filtro simple que protege a tabela inteira de EmployeeSecurity de consulta por qualquer usuário que seja membro da função.  
  
> [!NOTE]  
> A função Sales Employees by Territory criada nesta lição restringe os membros a procurar (ou consultar) apenas dados de vendas para a região de vendas à qual eles pertencem. Se você adicionar um usuário como um membro dos funcionários de vendas por função de território que também existe como um membro em uma função criada em [lição 11: criar funções](../analysis-services/lesson-11-create-roles.md), você obterá uma combinação de permissões. Quando um usuário for membro de várias funções, as permissões e os filtros de linha definidas para cada função serão cumulativos. Quer dizer, o usuário terá as maiores permissões determinadas pela combinação de funções.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Para criar uma função de usuário Sales Employees by Territory  
  
1.  No SSDT, clique no **modelo** menu e clique **funções**.  
  
2.  Em **Gerenciador de funções**, clique em **novo**.  
  
    Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, na coluna **Nome** , renomeie a função como **Funcionários de Vendas por Região**.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** .  
  
5.  Clique na guia **Membros** e em **Adicionar**.  
  
6.  No **Selecionar usuário ou grupo** na caixa **insira o nome de objeto para selecionar**, digite o primeiro nome de usuário de exemplo usado ao criar a tabela de EmployeeSecurity. Clique em **Verificar Nomes** para verificar se o nome de usuário é válido e clique em **OK**.  
  
    Repita essa etapa, adicionando os outros nomes de usuário amostra usada ao criar a tabela de EmployeeSecurity.  
  
7.  Clique na guia **Filtros de Linha** .  
  
8.  Para o **EmployeeSecurity** tabela, o **filtro DAX** coluna, digite a fórmula a seguir.  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula Especifica que todas as colunas são resolvidas para a condição booliana false; Portanto, não há colunas para a tabela EmployeeSecurity podem ser consultadas por um membro dos funcionários de vendas por função de usuário de território.  
  
9. Na tabela **DimSalesTerritory** , digite a fórmula a seguir.  

    ```  
    ='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 
      'Employee Security'[Login Id], USERNAME(), 
      'Employee Security'[Sales Territory Id], 
      'Sales Territory'[Sales Territory Id]) 
    ```
  
    Nesta fórmula, a função LOOKUPVALUE retorna todos os valores para a coluna DimEmployeeSecurity [SalesTerritoryId], onde o EmployeeSecurity [LoginId] é o mesmo que o nome de usuário do Windows de logon atual e EmployeeSecurity [SalesTerritoryId] é o mesmo que o DimSalesTerritory [SalesTerritoryId].  
  
    O conjunto de IDs retornados por LOOKUPVALUE de território de vendas, em seguida, é usado para restringir as linhas mostradas na tabela DimSalesTerritory. Somente as linhas onde SalesTerritoryID para a linha estiver no conjunto de IDs retornadas pela função LOOKUPVALUE são exibidas.  
  
10. No Gerenciador de função, clique em **Okey**.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Testar a função de usuário Sales Employees by Territory  
Nesta tarefa, você usará o analisar no recurso do Excel no SSDT para testar a eficácia dos funcionários de vendas por função de usuário de território. Você especificará um dos nomes de usuário adicionada à tabela EmployeeSecurity e como um membro da função. Este nome de usuário será usado como o nome de usuário efetivo na conexão criada entre o Excel e o modelo.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Para testar a função de usuário Sales Employees by Territory  
  
1.  No SSDT, clique no **modelo** menu e clique **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , em **Especifique o nome de usuário ou a função a ser usada para conectar-se ao modelo**, selecione **Outro Usuário do Windows**e clique em **Procurar**.  
  
3.  No **Selecionar usuário ou grupo** na caixa **insira o nome do objeto para selecionar**, digite um dos nomes de usuário incluídos na tabela EmployeeSecurity e, em seguida, clique em **verificar nomes**.  
  
4.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Usuário ou Grupo** e clique em **OK** para fechar a caixa de diálogo **Analisar no Excel** .  
  
    O Excel será aberto com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. A lista PivotTable Fields inclui a maioria dos campos de dados disponíveis no novo modelo.  
  
    Observe que a tabela de EmployeeSecurity não está visível na lista PivotTable Fields. Isso ocorre porque você optou por ocultar esta tabela de ferramentas de cliente em uma tarefa anterior.  
  
5.  No **campos** listar, **∑ Internet Sales** (medidas), selecione o **InternetTotalSales** medidas. A medida será inserida nos campos **Valores** .  
  
6.  Selecione o **SalesTerritoryId** coluna a partir de **DimSalesTerritory** tabela. A coluna será inserida nos campos **Rótulos de Linha** .  
  
    Note que valores de vendas pela Internet aparecem apenas para a uma região à qual pertence o nome de usuário efetivo que você usou. Se você selecionar outra coluna. Por exemplo, City, da tabela DimGeography como campo Row Label, apenas as cidades da região de vendas ao qual pertence o usuário efetivo são exibidos.  
  
    Este usuário não pode navegar nem consultar dados de vendas pela Internet regiões que não sejam aquela à qual eles pertencem porque o filtro de linha definido para a tabela Sales Territory na função de usuário Sales Employees by Territory efetivamente protege dados para todos os dados relacionados a outras regiões de vendas.  
  
## <a name="see-also"></a>Consulte também  
[Função USERNAME (DAX)](http://msdn.microsoft.com/en-us/22dddc4b-1648-4c89-8c93-f1151162b93f)  
[Função LOOKUPVALUE (DAX)](http://msdn.microsoft.com/en-us/73a51c4d-131c-4c33-a139-b1342d10caab)  
[Função CUSTOMDATA (DAX)](http://msdn.microsoft.com/en-us/58235ad8-226c-43cc-8a69-5a52ac19dd4e)  
