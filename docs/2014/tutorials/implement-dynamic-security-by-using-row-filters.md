---
title: Implementar a segurança dinâmica usando filtros de linha | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 8bf03c45-caf5-4eda-9314-e4f8f24a159f
author: minewiskan
ms.author: owend
manager: kfile
ms.openlocfilehash: 39d0d92d83a41970dcddae54d74aca3d118dcf6f
ms.sourcegitcommit: e042272a38fb646df05152c676e5cbeae3f9cd13
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/27/2020
ms.locfileid: "69530880"
---
# <a name="implement-dynamic-security-by-using-row-filters"></a>Implementar a segurança dinâmica usando filtros de linha
  Nesta lição suplementar, você criará uma função adicional que implementa a segurança dinâmica. A segurança dinâmica oferece segurança no nível de linha com base no nome de usuário ou na ID de logon do usuário conectado no momento. Para obter mais informações, consulte [Funções &#40;SSAS Tabular&#41;](https://docs.microsoft.com/analysis-services/tabular-models/roles-ssas-tabular).  
  
 Para implementar a segurança dinâmica, você deverá adicionar uma tabela a seu modelo contendo os nomes de usuários Windows desses usuários que podem criar uma conexão com o modelo como uma fonte de dados e procurar objetos e dados do modelo. O modelo criado usando este tutorial está no contexto da Adventure Works Corp.; entretanto, para concluir esta lição, você deve adicionar uma tabela contendo os usuários de seu próprio domínio. Você não precisará das senhas para os nomes de usuários que serão adicionados. Para criar uma tabela Employee Security, com um exemplo pequeno de usuários de seu próprio domínio, você usará o recurso Colar, colando dados de funcionário de uma planilha do Excel. Em um cenário do mundo real, a tabela que contém nomes de usuários adicionada a um modelo normalmente empregaria uma tabela de um banco de dados real como uma fonte de dados; por exemplo, uma tabela real dimEmployee.  
  
 Para implementar a segurança dinâmica, você usará duas novas funções DAX: [função de nome de usuário &#40;dax&#41;](/dax/username-function-dax) e [lookupvalue função &#40;Dax&#41;](/dax/lookupvalue-function-dax). Essas funções, aplicadas em uma fórmula de filtro de linha, são definidas em uma nova função. Usando a função LOOKUPVALUE, a fórmula especifica um valor da tabela Employee Security e passa esse valor para a função USERNAME, que especifica o nome de usuário do usuário registrado que pertence a esta função. O usuário pode procurar somente os dados especificados pelos filtros de linha da função. Neste cenário, você especificará que os funcionários de vendas só podem procurar dados de vendas pela internet para as regiões de vendas das quais eles são membro.  
  
 Para concluir esta lição suplementar, você executará uma série de tarefas. Aquelas tarefas que são exclusivas deste cenário de modelo tabular da Adventure Works, mas que não seriam aplicariam necessariamente a um cenário do mundo real, são identificadas como tal. Cada tarefa inclui informações adicionais que descrevem o propósito da tarefa.  
  
 Tempo estimado para conclusão desta lição: **30 minutos**  
  
## <a name="prerequisites"></a>Pré-requisitos  
 Este tópico de lição suplementar faz parte de um tutorial de modelagem tabular, que deve ser concluído na devida ordem. Antes de executar as tarefas nesta lição suplementar, você deve ter concluído todas as lições anteriores.  
  
## <a name="add-the-dimsalesterritory-table-to-the-aw-internet-sales-tabular-model-project"></a>Adicione a tabela dimSalesTerritory ao Projeto de Modelo de Tabela de Vendas pela Internet da AW  
 Para implementar a segurança dinâmica para este cenário do Adventure Works, inclua duas tabelas adicionais no seu modelo. A primeira tabela que você adicionará é dimSalesTerritory (como Sales Territory) do mesmo banco de dados AdventureWorksDW. Você aplicará um filtro de linha posteriormente à tabela Sales Territory que define os dados específicos que o usuário registrado pode procurar.  
  
#### <a name="to-add-the-dimsalesterritory-table"></a>Para adicionar a tabela dimSalesTerritory  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Conexões Existentes**.  
  
2.  Na caixa de diálogo **Conexões Existentes** , verifique se a conexão da fonte de dados **Adventure Works DB do SQL** está selecionada e clique em **Abrir**.  
  
     Se a caixa de diálogo Credenciais de Representação aparecer, digite as credenciais de representação usadas na Lição 2: adicionar dados.  
  
3.  Na página **Escolher Como Importar os Dados** , deixe marcada a opção **Selecionar itens em uma lista de tabelas e exibições para escolher os dados a serem importados** e clique em **Avançar**.  
  
4.  Na página **Selecionar Tabelas e Exibições** , selecione a tabela **DimSalesTerritory** .  
  
5.  Na coluna Nome Amigável, digite **Região de Vendas**.  
  
6.  Clique em **Visualizar e Filtrar**.  
  
7.  Desmarque a coluna **SalesTerritoryAlternateKey** e clique em **OK**.  
  
8.  Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
     A nova tabela será adicionada ao workspace do modelo. Objetos e dados da tabela de origem dimSalesTerritory são importados para a nova tabela Sales Territory em seu Modelo de Tabela de Vendas pela Internet AW.  
  
9. Depois que a tabela for importada, clique em **Fechar**.  
  
## <a name="give-the-columns-friendly-names"></a>Atribuir os nomes amigáveis de colunas  
 Nesta tarefa, você renomeará as colunas na tabela Sales Territory, atribuindo-lhes nomes amigáveis. Nem sempre é necessário atribuir nomes amigáveis a tabelas e/ou colunas; no entanto, isso facilita a navegação do seu projeto de modelo no designer de modelo, bem como a procura de objetos de modelo e os dados em uma lista de campos do aplicativo cliente.  
  
#### <a name="to-rename-columns-in-the-sales-territory-table"></a>Para renomear Colunas na Tabela Sales Territory  
  
-   No designer de modelos, renomeie as colunas da tabela **Região de Vendas** :  
  
     **Sales Territory**  
  
    |Nome de origem|Nome amigável|  
    |-----------------|-------------------|  
    |SalesTerritoryKey|Sales Territory Id|  
    |SalesTerritoryRegion|Sales Territory Region|  
    |SalesTerritoryCountry|Sales Territory Country|  
    |SalesTerritoryGroup|Sales Territory Group|  
  
## <a name="add-a-table-with-user-name-data"></a>Adicionar uma tabela com os dados de nome de usuário  
 Como a tabela dimEmployee no banco de dados de exemplo AdventureWorksDW contém usuários do domínio AdventureWorks, e esses nomes de usuários não existem em seu próprio ambiente, crie uma tabela em seu modelo que contenha um exemplo pequeno (três) de usuários reais de sua organização. Você adicionará estes usuários como membros à nova função. Você não precisa das senhas para os nomes de usuários de exemplo, mas precisará dos nomes de usuários reais do Windows de seu próprio domínio.  
  
#### <a name="to-add-an-employee-security-table"></a>Para adicionar uma tabela Segurança de Funcionário  
  
1.  Abra o Microsoft Excel e crie uma nova planilha.  
  
2.  Copie a tabela a seguir incluindo a linha de cabeçalho e cole-a na planilha.  
  
    |Employee Id|Sales Territory Id|Nome|Sobrenome|Login Id|  
    |-----------------|------------------------|----------------|---------------|--------------|  
    |1|2|\<nome do usuário>|\<> do último nome do usuário|\<domínio \ nomedeusuário>|  
    |1|3|\<nome do usuário>|\<> do último nome do usuário|\<domínio \ nomedeusuário>|  
    |2|4|\<nome do usuário>|\<> do último nome do usuário|\<domínio \ nomedeusuário>|  
    |3|5|\<nome do usuário>|\<> do último nome do usuário|\<domínio \ nomedeusuário>|  
  
3.  Na nova planilha, substitua o nome, o sobrenome e o domínio\nome de usuário pelos nomes e ids de logon de três usuários em sua organização. Coloque o mesmo usuário nas duas primeiras linhas, para Employee Id 1. Isso mostrará que este usuário pertence a mais de uma região de vendas. Deixe os campos Employee Id e Sales Territory Id como tal.  
  
4.  Salve a planilha como `Sample Employee`.  
  
5.  Na planilha, selecione todas as células com dados de funcionário, incluindo os cabeçalhos, clique com o botão direito do mouse nos dados selecionados e clique em **Copiar**.  
  
6.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Editar** e em **Colar**.  
  
     Se a opção Colar estiver acinzentada, clique em qualquer coluna de qualquer tabela na janela do designer de modelos, clique no menu **Editar** e em **Colar**.  
  
7.  Na caixa de diálogo **visualização de colagem** , em **nome**da tabela `Employee Security`, digite.  
  
8.  Em **Dados a serem colados**, verifique se os dados incluem todos os dados de usuário e cabeçalhos da planilha Funcionário de Exemplo.  
  
9. Verifique se a opção **Usar primeira linha como cabeçalhos de coluna** está marcada e clique em **Ok**.  
  
     Uma nova tabela nomeada Employee Security com dados de funcionário copiados da planilha Sample Employee é criada.  
  
## <a name="create-relationships-between-internet-sales-geography-and-sales-territory-table"></a>Criar relações entre as tabelas Internet Sales, Geography e Sales Territory  
 A tabela vendas pela Internet, Geografia e região de vendas contém uma coluna comum, ID da região de vendas. A coluna ID da região de vendas na tabela região de vendas contém valores com uma ID diferente para cada região de vendas.  
  
#### <a name="to-create-relationships-between-the-internet-sales-geography-and-the-sales-territory-table"></a>Para criar relações entre as tabelas Internet Sales, Geography e Sales Territory  
  
1.  No designer de modelos, em Exibição de Diagrama, na tabela **Geografia** , clique e mantenha o botão do mouse pressionado na coluna **ID da Região de Vendas** , arraste o cursor até a coluna **ID da Região de Vendas** da tabela **Região de Vendas** e solte o botão.  
  
2.  Na tabela **Vendas pela Internet** , clique e mantenha o botão do mouse pressionado na coluna **ID da Região de Vendas** , arraste o cursor até a coluna **ID da Região de Vendas** da tabela **Região de Vendas** e solte o botão.  
  
     Note que a propriedade ativa desta relação é False, o que significa que ela está inativa. Isso ocorre porque a tabela Internet Sales já tem outra relação ativa que é usada em medidas.  
  
## <a name="hide-the-employee-security-table-from-client-applications"></a>Ocultar a tabela Employee Security de aplicativos cliente  
 Nesta tarefa, você ocultará a tabela de segurança do funcionário, impedindo que ela apareça na lista de campos de um aplicativo cliente. Lembre-se que ocultar uma tabela não a protege. Os usuários ainda poderão consultar dados da tabela Employee Security se souberem como fazê-lo. Para proteger os dados da tabela Employee Security, impedindo que usuários possam consultar seus dados, você aplicará um filtro em uma tarefa posterior.  
  
#### <a name="to-hide-the-employee-table-from-client-applications"></a>Para ocultar a tabela Employee de aplicativos cliente  
  
-   No designer de modelos, na Exibição de Diagrama, clique com o botão direito do mouse no título de tabela **Funcionário** e, em seguida, clique em **Ocultar das Ferramentas de Cliente**.  
  
## <a name="create-a-sales-employees-by-territory-user-role"></a>Criar uma função de usuário de Funcionários de Vendas por Região  
 Nesta tarefa, você criará uma nova função de usuário. Esta função incluirá um filtro de linha que define quais linhas da tabela Sales Territory são visíveis a usuários. O filtro é aplicado na direção de relação um para muitos a todas as outras tabelas relacionadas a Sales Territory. Você também aplicará um filtro simples que protege a tabela Employee Security inteira contra a consulta por qualquer usuário que seja membro da função.  
  
> [!NOTE]  
>  A função Funcionários de Vendas por Região criada nesta lição restringe os membros para procurar (ou consultar) apenas dados de vendas da região de vendas à qual pertencem. Se você adicionar um usuário como um membro à função Funcionários de Vendas por Região que também existe como um membro em uma função criada na [Lição 12: Criar funções](../analysis-services/lesson-11-create-roles.md), você obterá uma combinação de permissões. Quando um usuário é um membro de várias funções, permissões e filtros de linha definidos para cada função são cumulativos. Quer dizer, o usuário terá as maiores permissões determinadas pela combinação de funções.  
  
#### <a name="to-create-a-sales-employees-by-territory-user-role"></a>Para criar uma função de usuário de Funcionários de Vendas por Região  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Funções**.  
  
2.  Na caixa de diálogo **Gerenciador de Funções** , clique em **Novo**.  
  
     Uma nova função com a permissão Nenhum é adicionada à lista.  
  
3.  Clique na nova função e, na coluna **nome** , renomeie a função como `Sales Employees by Territory`.  
  
4.  Na coluna **Permissões**, clique na lista suspensa e, em seguida, selecione a permissão **Leitura**.  
  
5.  Clique na guia **Membros** e em **Adicionar**.  
  
6.  Na caixa de diálogo **Selecionar Usuário ou Grupo** , em **Inserir o objeto nomeado a ser selecionado**, digite o primeiro nome de usuário de exemplo que você usou ao criar a tabela Segurança do Funcionário. Clique em **Verificar Nomes** para verificar se o nome de usuário é válido e, em seguida, clique em **Ok**.  
  
     Repita esta etapa, adicionando os outros nomes de usuários de exemplo usados ao criar a tabela Employee Security.  
  
7.  Clique na guia **Filtros de Linha** .  
  
8.  Para a `Employee Security` tabela, na coluna **filtro Dax** , digite a fórmula a seguir.  
  
     `=FALSE()`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
     Esta fórmula especifica que todas as colunas são resolvidas com a condição Booliana false; portanto, nenhuma coluna da tabela Employee Security pode ser consultada por um membro da função de usuário Sales Employees by Territory.  
  
9. Na tabela **Região de Vendas** , digite a fórmula a seguir.  
  
     `='Sales Territory'[Sales Territory Id]=LOOKUPVALUE('Employee Security'[Sales Territory Id], 'Employee Security'[Login Id], USERNAME(), 'Employee Security'[Sales Territory Id], 'Sales Territory'[Sales Territory Id])`  
  
     Ao concluir a criação da fórmula, pressione ENTER.  
  
     Nesta fórmula, a função LOOKUPVALUE retorna todos os valores da coluna Employee Security[Sales Territory Id], onde Employee Security[Login Id] equivale ao nome de usuário atual registrado no Windows, e Employee Security[Sales Territory Id] equivale ao Sales Territory[Sales Territory Id].  
  
     O conjunto de Sales Territory IDs retornado por LOOKUPVALUE é usado para restringir as linhas mostradas na tabela Sales Territory. Apenas as linhas em que Sales Territory ID para a linha estiver no conjunto de IDs retornadas pela função LOOKUPVALUE são exibidas.  
  
10. Na caixa de diálogo Gerenciador de Funções, clique em **OK**.  
  
## <a name="test-the-sales-employees-by-territory-user-role"></a>Testar a função de usuário de Funcionários de Vendas por Região  
 Nesta tarefa, você usará o recurso Analisar no Excel no [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)] para testar a eficácia da função de usuário Sales Employees by Territory. Você especificará um dos nomes de usuários adicionado à tabela Employee Security e como um membro da função. Este nome de usuário será usado como o nome de usuário efetivo na conexão criada entre o Excel e o modelo.  
  
#### <a name="to-test-the-sales-employees-by-territory-user-role"></a>Para testar a função de usuário de Funcionários de Vendas por Região  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], clique no menu **Modelo** e em **Analisar no Excel**.  
  
2.  Na caixa de diálogo **Analisar no Excel**, **especifique o nome de usuário ou função a ser usada para se conectar ao modelo**, selecione **Outro Usuário do Windows** e, em seguida, clique em **Procurar**.  
  
3.  Na caixa de diálogo **Selecionar Usuário ou Grupo** , em **Inserir o nome de objeto a ser selecionado**, digite um dos nomes de usuário incluídos na tabela Funcionário e clique em **Verificar Nomes**.  
  
4.  Clique em **Ok** para fechar a caixa de diálogo **Selecionar Usuário ou Grupo** e clique em **Ok** para fechar a caixa de diálogo **Analisar no Excel**.  
  
     O Excel abrirá uma nova pasta de trabalho. Uma Tabela Dinâmica é criada automaticamente. A Lista de Campos de Tabela Dinâmica inclui a maioria dos campos de dados disponíveis no novo modelo.  
  
     Note que a tabela Employee Security não fica visível na Lista de campos de Tabela Dinâmica. Isso ocorre porque você optou por ocultar esta tabela de ferramentas de cliente em uma tarefa anterior.  
  
5.  Na lista **Campo da Tabela Dinâmica** , em **∑ Vendas pela Internet** (medidas), selecione a medida **Total de Vendas pela Internet** . A medida será inserida nos campos **Valores** .  
  
6.  Na lista **Campo da Tabela Dinâmica** , selecione a coluna **ID da Região de Vendas** da tabela **Região de Vendas** . A coluna será inserida nos campos **Rótulos de Linha** .  
  
     Observe que os valores de vendas pela Internet aparecem somente para a região à qual o nome de usuário efetivo usado pertence. Se você selecionar outra coluna; por exemplo, City, da tabela Geography como campo Row Label, apenas as cidades da região de vendas à qual o usuário efetivo pertence serão exibidas.  
  
     Este usuário não pode navegar nem consultar dados de vendas pela Internet regiões que não sejam aquela à qual eles pertencem porque o filtro de linha definido para a tabela Sales Territory na função de usuário Sales Employees by Territory efetivamente protege dados para todos os dados relacionados a outras regiões de vendas.  
  
## <a name="see-also"></a>Consulte Também  
 [Função de nome de usuário &#40;DAX&#41;](/dax/username-function-dax)   
 [Função LOOKUPvalue &#40;DAX&#41;](/dax/lookupvalue-function-dax)   
 [Função CUSTOMDATA &#40;DAX&#41;](/dax/customdata-function-dax)  
  
  
