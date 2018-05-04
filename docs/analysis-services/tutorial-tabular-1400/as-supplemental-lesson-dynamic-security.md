---
title: 'Lição suplementar do Analysis Services tutorial: segurança dinâmica | Microsoft Docs'
description: Descreve como usar a segurança dinâmica usando filtros de linha no tutorial do Analysis Services.
ms.prod_service: analysis-services, azure-analysis-services
services: analysis-services
ms.suite: pro-bi
documentationcenter: ''
author: Minewiskan
manager: kfile
editor: ''
tags: ''
ms.assetid: ''
ms.service: analysis-services
ms.devlang: NA
ms.topic: get-started-article
ms.tgt_pltfrm: NA
ms.date: 02/20/2018
ms.author: owend
monikerRange: '>= sql-analysis-services-2017 || = sqlallproducts-allversions'
ms.openlocfilehash: ffd58456ee40741792ac7ce409c97e064a92ba43
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="supplemental-lesson---dynamic-security"></a>Lição suplementar - segurança dinâmica

[!INCLUDE[ssas-appliesto-sql2017-later-aas](../../includes/ssas-appliesto-sql2017-later-aas.md)]

Esta lição suplementar, você cria uma função adicional que implementa a segurança dinâmica. A segurança dinâmica oferece segurança em nível de linha com base no nome de usuário ou na id de logon do usuário conectado no momento. 
  
Para implementar a segurança dinâmica, você pode adicionar uma tabela para seu modelo que contém os nomes de usuários que podem se conectar ao modelo e procurar dados e objetos de modelo. O modelo que você cria usando este tutorial está no contexto da Adventure Works; No entanto, para concluir esta lição, você deve adicionar uma tabela que contém os usuários de seu próprio domínio. As senhas não é necessário para os nomes de usuário que são adicionados. Para criar uma tabela de EmployeeSecurity, com uma pequena amostra dos usuários de seu próprio domínio, use o recurso Colar, colando dados de funcionários de uma planilha do Excel. Em um cenário do mundo real, a tabela que contém os nomes de usuário normalmente seria uma tabela de banco de dados real como uma fonte de dados; Por exemplo, uma tabela DimEmployee real.  
  
Para implementar a segurança dinâmica, você usar duas funções DAX: [função USERNAME (DAX)](http://msdn.microsoft.com/22dddc4b-1648-4c89-8c93-f1151162b93f) e [função LOOKUPVALUE (DAX)](http://msdn.microsoft.com/73a51c4d-131c-4c33-a139-b1342d10caab). Estas funções, aplicadas em um fórmula de filtro de linha, são definidas em uma nova função. Usando a função LOOKUPVALUE, a fórmula Especifica um valor da tabela EmployeeSecurity. A fórmula, em seguida, passa a que o valor para a função de nome de usuário, que especifica o nome de usuário do usuário conectado pertence a essa função. O usuário pode procurar apenas nos dados especificados pelos filtros de linha da função. Nesse cenário, você especificar que os funcionários de vendas só podem procurar dados de vendas pela Internet para as regiões de vendas em que eles são membros.  
  
Essas tarefas que são exclusivas deste cenário de modelo de tabela do Adventure Works, mas não se aplicariam necessariamente a um cenário do mundo real, são identificadas como tal. Cada tarefa inclui informações adicionais que descrevem o propósito da tarefa.  
  
Tempo estimado para concluir esta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Prerequisites  

Este artigo lição suplementar faz parte de um tutorial de modelagem de tabela, que deve ser concluído na ordem. Antes de executar as tarefas desta lição suplementar, conclua todas as lições anteriores.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Adicione a tabela dimSalesTerritory ao Projeto de Modelo de Tabela de Vendas pela Internet da AW  

Para implementar a segurança dinâmica para este cenário do Adventure Works, você deve adicionar duas tabelas adicionais ao seu modelo. A primeira tabela que você adicionar é DimSalesTerritory (como Sales Territory) do mesmo banco de dados AdventureWorksDW. Posteriormente, você aplicar um filtro de linha à tabela SalesTerritory que define os dados específicos que do usuário conectado pode procurar.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Para adicionar a tabela dimSalesTerritory  
  
1.  No Gerenciador de modelos de tabela > **fontes de dados**, clique com botão direito sua conexão e, em seguida, clique em **importar novas tabelas**.  

    Se a caixa de diálogo Credenciais de Representação aparecer, digite as credenciais de representação usadas na Lição 2: Adicionar dados.
  
2.  No navegador, selecione o **DimSalesTerritory** de tabela e, em seguida, clique em **Okey**.    
  
3.  No Editor de consultas, clique o **DimSalesTerritory** de consulta e, em seguida, remover **SalesTerritoryAlternateKey** coluna.  
  
7.  Clique em **Importar**.  
  
    A nova tabela será adicionada ao espaço de trabalho do modelo. Objetos e dados da tabela de origem DimSalesTerritory, em seguida, são importados para o modelo de tabela de vendas de Internet AW.  
  
9. Depois que a tabela foi importada com êxito, clique em **fechar**.  

## <a name="add-a-table-with-user-name-data"></a>Adicione uma tabela com dados de nome de usuário  

A tabela DimEmployee no banco de dados de exemplo AdventureWorksDW contém usuários do domínio AdventureWorks. Esses nomes de usuários não existem no seu ambiente. Você deve criar uma tabela em seu modelo que contenha um exemplo pequeno (pelo menos três) de usuários reais de sua organização. Em seguida, adicione esses usuários como membros à nova função. Você não precisa as senhas para os exemplos de nomes de usuário, mas você precisa nomes de usuário do Windows reais de seu próprio domínio.  
  
#### <a name="to-add-an-employeesecurity-table"></a>Para adicionar uma tabela EmployeeSecurity  
  
1.  Abra o Microsoft Excel, criar uma planilha.  
  
2.  Copie a tabela a seguir, inclusive a linha de cabeçalho, e cole-a na planilha.  

    ```
      |EmployeeId|SalesTerritoryId|FirstName|LastName|LoginId|  
      |---------------|----------------------|--------------|-------------|------------|  
      |1|2|<user first name>|<user last name>|\<domain\username>|  
      |1|3|<user first name>|<user last name>|\<domain\username>|  
      |2|4|<user first name>|<user last name>|\<domain\username>|  
      |3|5|<user first name>|<user last name>|\<domain\username>|  
    ```

3.  Substitua o nome, sobrenome e domínio ome de usuário com os nomes e ids de logon de três usuários em sua organização. Coloque o mesmo usuário nas duas primeiras linhas, para 1 EmployeeId, mostrando a que este usuário pertence a mais de uma região de vendas. Deixe os campos EmployeeId e SalesTerritoryId como estão.  
  
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
  
1.  Na exibição de diagrama no **DimGeography** de tabela, clique e mantenha o **SalesTerritoryId** coluna, em seguida, arraste o cursor para o **SalesTerritoryId** coluna no **DimSalesTerritory** de tabela e, em seguida, solte.  
  
2.  No **FactInternetSales** de tabela, clique e mantenha o **SalesTerritoryId** coluna, em seguida, arraste o cursor para o **SalesTerritoryId** coluna no **DimSalesTerritory** de tabela e, em seguida, solte.  
  
    Observe que a propriedade ativa desta relação é False, o que significa que ele está inativo. A tabela FactInternetSales já tem outra relação ativa.  
  
## <a name="hide-the-employeesecurity-table-from-client-applications"></a>Ocultar a tabela de EmployeeSecurity de aplicativos cliente  

Nesta tarefa, você ocultar tabela EmployeeSecurity, impedindo que ela apareça na lista de campos de um aplicativo cliente. Tenha em mente que, ao ocultar uma tabela não proteger. Os usuários podem consultar os dados da tabela EmployeeSecurity ainda se souberem como. Para proteger os dados da tabela EmployeeSecurity, impedindo que os usuários possam consultar seus dados, você deve aplicar um filtro em uma tarefa posterior.  
  
#### <a name="to-hide-the-employeesecurity-table-from-client-applications"></a>Para ocultar a tabela de EmployeeSecurity de aplicativos cliente  
  
-   No designer de modelos, em Exibição de Diagrama, clique com o botão direito do mouse no cabeçalho da tabela **Funcionário** e clique em **Ocultar das Ferramentas de Cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Criar uma função de usuário Sales Employees by Territory  

Nesta tarefa, você deve criar uma função de usuário. Essa função inclui um filtro de linha que define quais linhas da tabela DimSalesTerritory são visíveis aos usuários. O filtro é aplicado, em seguida, na direção para todas as outras tabelas relacionadas à DimSalesTerritory relação um-para-muitos. Você também pode aplicar um filtro que protege a tabela inteira de EmployeeSecurity de consulta por qualquer usuário que seja membro da função.  
  
> [!NOTE]  
> A função Sales Employees by Territory criada nesta lição restringe os membros a procurar (ou consultar) apenas dados de vendas para a região de vendas à qual eles pertencem. Se você adicionar um usuário como um membro dos funcionários de vendas por função de território que também existe como um membro em uma função criada em [lição 11: criar funções](../tutorial-tabular-1400/as-lesson-11-create-roles.md), você obtém uma combinação de permissões. Quando um usuário for membro de várias funções, as permissões e os filtros de linha definidas para cada função serão cumulativos. Ou seja, o usuário tem as maiores permissões determinadas pela combinação de funções.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Para criar uma função de usuário Sales Employees by Territory  
  
1.  No SSDT, clique no **modelo** menu e clique **funções**.  
  
2.  Em **Gerenciador de funções**, clique em **novo**.  
  
    Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique em nova função e, em seguida, no **nome** coluna, renomeie a função para **funcionários de vendas por território**.  
  
4.  Na coluna **Permissões** , clique na lista suspensa e selecione a permissão **Leitura** .  
  
5.  Clique o **membros** guia e, em seguida, clique em **adicionar**.  
  
6.  No **Selecionar usuário ou grupo** na caixa **insira o nome de objeto para selecionar**, digite o primeiro nome de usuário de exemplo usado ao criar a tabela de EmployeeSecurity. Clique em **Verificar Nomes** para verificar se o nome de usuário é válido e clique em **OK**.  
  
    Repita essa etapa, adicionando os outros nomes de usuário amostra usada ao criar a tabela de EmployeeSecurity.  
  
7.  Clique o **filtros de linha** guia.  
  
8.  Para o **EmployeeSecurity** tabela, o **filtro DAX** coluna, digite a seguinte fórmula:  
  
    ```
      =FALSE()  
    ```
  
    Esta fórmula Especifica que todas as colunas são resolvidas para a condição booliana false. Não há colunas para a tabela de EmployeeSecurity podem ser consultadas por um membro dos funcionários de vendas por função de usuário de território.  
  
9. Para o **DimSalesTerritory** da tabela, digite a seguinte fórmula:  

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

Nesta tarefa, você usa o recurso analisar no Excel no SSDT para testar a eficácia dos funcionários de vendas por função de usuário de território. Você especificar um dos nomes de usuário que você adicionou à tabela EmployeeSecurity e como um membro da função. Este nome de usuário, em seguida, é usado como o nome de usuário efetivo na conexão criada entre o Excel e o modelo.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Para testar a função de usuário Sales Employees by Territory  
  
1.  No SSDT, clique no **modelo** menu e clique **analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel** , em **Especifique o nome de usuário ou a função a ser usada para conectar-se ao modelo**, selecione **Outro Usuário do Windows**e clique em **Procurar**.  
  
3.  No **Selecionar usuário ou grupo** na caixa **insira o nome do objeto para selecionar**, digite um nome de usuário incluídos na tabela EmployeeSecurity e, em seguida, clique em **verificar nomes**.  
  
4.  Clique em **OK** para fechar a caixa de diálogo **Selecionar Usuário ou Grupo** e clique em **OK** para fechar a caixa de diálogo **Analisar no Excel** .  
  
    O Excel abre com uma nova pasta de trabalho. Uma tabela dinâmica é criada automaticamente. A lista PivotTable Fields inclui a maioria dos campos de dados disponíveis no novo modelo.  
  
    Observe que a tabela de EmployeeSecurity não está visível na lista PivotTable Fields. Você ocultou essa tabela das ferramentas de cliente em uma tarefa anterior.  
  
5.  No **campos** listar, **∑ Internet Sales** (medidas), selecione o **InternetTotalSales** medidas. A medida é inserida no **valores** campos.  
  
6.  Selecione o **SalesTerritoryId** coluna a partir de **DimSalesTerritory** tabela. A coluna é inserida no **rótulos de linha** campos.  
  
    Note que valores de vendas pela Internet aparecem apenas para a uma região à qual pertence o nome de usuário efetivo que você usou. Se você selecionar outra coluna, como cidade da tabela DimGeography de campo de rótulo de linha, são exibidas apenas as cidades da região de vendas ao qual pertence o usuário efetivo.  
    Este usuário não pode pesquisar ou consultar qualquer dados de vendas pela Internet para regiões que não pertencem a. Essa restrição é porque o filtro de linha definido para a tabela DimSalesTerritory, em que os funcionários de vendas por função de usuário de território, protege os dados para todos os dados relacionados a outros territórios de vendas.  
  
## <a name="see-also"></a>Consulte também  

[Função USERNAME (DAX)](https://msdn.microsoft.com/library/hh230954.aspx)  
[Função LOOKUPVALUE (DAX)](https://msdn.microsoft.com/library/gg492170.aspx)  
[Função CUSTOMDATA (DAX)](https://msdn.microsoft.com/library/hh213140.aspx)  
