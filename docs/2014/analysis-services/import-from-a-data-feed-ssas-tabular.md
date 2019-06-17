---
title: Importar de um Feed de dados (SSAS Tabular) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 0686e519-67c2-4f9b-8cd2-84a4871499ee
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: bcb3a1cbcabc66492bbd780be4716ce69f15de37
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66080568"
---
# <a name="import-from-a-data-feed-ssas-tabular"></a>Importar de um feed de dados (SSAS tabular)
  Feeds de dados são um ou mais fluxos de dados XML gerados a partir de uma fonte de dados online e transmitidos para um documento ou aplicativo de destino. Você pode importar dados de um feed de dados para o modelo usando o Assistente de Importação de Tabela.  
  
 Este tópico contém as seguintes seções:  
  
-   [Compreendendo a importação de um feed de dados](#prereq)  
  
-   [Importe os dados de um conjunto de dados do Azure DataMarket](#azure)  
  
-   [Importar feeds de dados de fontes de dados públicas ou corporativas](#importdata)  
  
-   [Importar feeds de dados de listas do SharePoint](#importlist)  
  
-   [Importar feeds de dados de Relatórios do Reporting Services](#importreport)  
  
##  <a name="prereq"></a> Compreendendo a importação de um feed de dados  
 Você pode importar dados em um Modelo Tabular dos seguintes tipos de feeds de dados:  
  
 **Relatório do Reporting Services**  
 É possível usar um relatório do Reporting Services que foi publicado em um site do SharePoint ou em um servidor de relatório como uma fonte de dados em um modelo. Ao importar dados de uma Relatório do Reporting Services, você deve especificar um arquivo de definição de relatório (.rdl) como uma fonte de dados.  
  
 **Conjunto de dados do Azure DataMarket**  
 O Azure DataMarket é um serviço que fornece uma único mercado e canal de entrega para informações como serviços em nuvem. Os conjuntos de dados do Azure DataMarket exigem uma chave de conta em vez de uma conta de usuário do Windows.  
  
 **Feeds Atom**  
 O feed deve ser um feed Atom. Não há suporte para RSS feeds. O feed deve estar publicamente disponível ou você deve ter permissão para se conectar a ele com a conta do Windows com a qual você está conectado.  
  
 Os dados de um feed de dados são adicionados em um modelo uma vez durante a importação. Para obter dados atualizados do feed, você poderá atualizar os dados do designer de modelo ou configurar uma agenda de atualização de dados para o modelo depois que for implantado em uma instância de produção do Analysis Services. Para obter mais informações, consulte [Processar dados &#40;SSAS de Tabela&#41;](process-data-ssas-tabular.md).  
  
##  <a name="azure"></a> Importe os dados de um conjunto de dados do Azure DataMarket  
 Você pode importar dados de um Azure DataMarket como uma tabela em seu modelo.  
  
#### <a name="to-import-data-from-an-azure-datamarket-dataset"></a>Para importar os dados de um conjunto de dados do Azure DataMarket  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**. O Assistente de Importação de Tabela é aberto.  
  
2.  Na página **Conectar com uma fonte de dados** , em **Feeds de Dados**, selecione **Conjunto de dados do Azure DataMarket**e clique em **Avançar**.  
  
3.  Na página **Conectar a um conjunto de dados do Azure DataMarket** , em **Nome amigável**, digite um nome descritivo para o feed que você está acessando. Se você estiver importando vários feeds ou fontes de dados, o uso de nomes descritivos para a conexão poderá ajudá-lo a lembrar como a conexão é usada.  
  
4.  Em **URL do feed de dados**, digite o endereço para o feed de dados.  
  
5.  Em **Configurações de segurança**, em **Chave da conta**, digite uma chave da conta. Chaves de conta são usadas pelo Analysis Services para acessar as assinaturas do DataMarket.  
  
6.  Clique em **Testar Conexão** para ter certeza de que o feed está disponível. Alternativamente, você também pode clicar em **Avançado** para confirmar que a URL Base ou a URL do Documento de Serviço contém a consulta ou o documento de serviço que fornece o feed.  
  
7.  Clique em **Avançar** para continuar a importação.  
  
8.  Na página **Informações sobre Representação** , especifique as credenciais que o Analysis Services usará para se conectar à fonte de dados ao atualizar os dados e clique em **Avançar**. Estas credenciais são diferentes da Chave de conta.  
  
9. Na página **Selecionar Tabelas e Exibições** do assistente, no campo **Nome Amigável** , digite um nome descritivo que identifique a tabela que conterá esses dados após a importação  
  
10. Clique em **Visualizar e Filtro** para examinar os dados e alterar as seleções de coluna. Não é possível restringir as linhas importadas no feed de dados de relatório, mas é possível remover colunas desmarcando as caixas de seleção. Clique em **OK**.  
  
11. Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
##  <a name="importdata"></a> Importar feeds de dados de fontes de dados públicas ou corporativas  
 Você pode acessar feeds públicos ou criar serviços de dados personalizados que geram feeds Atom a partir de sistemas de banco de dados proprietários ou herdados.  
  
#### <a name="to-import-data-from-public-or-corporate-data-feeds"></a>Para importar dados de feeds de dados públicos ou corporativos  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**. O Assistente de Importação de Tabela é aberto.  
  
2.  Na página **Conectar com uma fonte de dados** , em **Feeds de Dados**, selecione **Outros Feeds**e clique em **Avançar**.  
  
3.  Na página **Conectar a um Feed de Dados** , digite um nome descritivo para o feed que você está acessando. Se você estiver importando vários feeds ou fontes de dados, o uso de nomes descritivos para a conexão poderá ajudá-lo a lembrar como a conexão é usada.  
  
4.  Em **URL do feed de dados**, digite o endereço para o feed de dados. Os valores válidos incluem os seguintes:  
  
    1.  Um documento XML que contém os dados Atom. Por exemplo, a seguinte URL aponta para um feed público no site Open Government Data Initiative:  
  
        ```  
        http://ogdi.cloudapp.net/v1/dc/banklocations/  
        ```  
  
    2.  Um documento .atomsvc que especifica um ou mais feeds. Um documento .atomsvc aponta para um serviço ou aplicativo que fornece um ou mais feeds. Cada feed é especificado como uma consulta básica que retorna o conjunto de resultados.  
  
         Você pode especificar um endereço de URL para um documento .atomsvc que esteja em um servidor Web ou pode abrir o arquivo de um compartilhou ou pasta local em seu computador. Você poderá ter um documento .atomsvc se salvou um arquivo desse tipo no computador ao exportar um relatório do Reporting Services ou pode ter documentos .atomsvc em uma biblioteca de feeds de dados que alguém criou para o site do SharePoint.  
  
        > [!NOTE]  
        >  É recomendável especificar um documento .atomsvc que possa ser acessado por meio de um endereço de URL ou pasta compartilhada porque isso lhe dá a opção de configurar a atualização de dados automática para a pasta de trabalho depois, após a publicação da pasta de trabalho no SharePoint. O servidor poderá reutilizar o mesmo endereço de URL ou pasta de rede para atualizar dados se você especificar um local que não seja local para o computador.  
  
5.  Clique em **Testar Conexão** para ter certeza de que o feed está disponível. Alternativamente, você também pode clicar em **Avançado** para confirmar que a URL Base ou a URL do Documento de Serviço contém a consulta ou o documento de serviço que fornece o feed.  
  
6.  Clique em **Avançar** para continuar a importação.  
  
7.  Na página **Informações sobre Representação** , especifique as credenciais que o Analysis Services usará para se conectar à fonte de dados ao atualizar os dados e clique em **Avançar**.  
  
8.  Na página **Selecionar Tabelas e Exibições** do assistente, no campo **Nome Amigável** , substitua Conteúdo do Feed de Dados por um nome descritivo que identifique a tabela que conterá esses dados após a importação  
  
9. Clique em **Visualizar e Filtro** para examinar os dados e alterar as seleções de coluna. Não é possível restringir as linhas importadas no feed de dados de relatório, mas é possível remover colunas desmarcando as caixas de seleção. Clique em **OK**.  
  
10. Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
##  <a name="importlist"></a> Importar feeds de dados de listas do SharePoint  
 Você pode importar qualquer lista do SharePoint que tenha um botão **Exportar como Feed de Dados** na faixa de opções (SharePoint). Você pode clicar nesse botão para exportar a lista como um feed.  
  
#### <a name="to-import-data-feeds-from-a-sharepoint-list"></a>Para importar feeds de dados de uma lista do SharePoint  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma fonte de dados** , em **Feeds de Dados**, selecione **Outros Feeds de Dados**e clique em **Avançar**.  
  
3.  Na página **Conectar a um Feed de Dados** , digite um nome descritivo para o feed que você está acessando. Se você estiver importando vários feeds ou fontes de dados, o uso de nomes descritivos para a conexão poderá ajudá-lo a lembrar como a conexão é usada.  
  
4.  Na URL do Feed de dados, digite um endereço para o serviço de dados de lista, substituindo \<server-name > pelo nome real do seu servidor do SharePoint:  
  
    ```  
    http://<server-name>/_vti_bin/listdata.svc  
    ```  
  
5.  Clique em **Testar Conexão** para ter certeza de que o feed está disponível. Alternativamente, você também pode clicar em **Avançado** para confirmar que a URL do Documento de Serviço contém um endereço para o serviço de dados da lista.  
  
6.  Clique em **Avançar** para continuar a importação.  
  
7.  Na página **Informações sobre Representação** , especifique as credenciais que o Analysis Services usará para se conectar à fonte de dados ao atualizar os dados e clique em **Avançar**.  
  
8.  Na página **Selecionar Tabelas e Exibições** do assistente, selecione as listas que você deseja importar.  
  
    > [!NOTE]  
    >  Somente é possível importar listas que contenham colunas.  
  
9. Clique em **Visualizar e Filtro** para examinar os dados e alterar as seleções de coluna. Não é possível restringir as linhas importadas no feed de dados de relatório, mas é possível remover colunas desmarcando as caixas de seleção. Clique em **OK**.  
  
10. Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
##  <a name="importreport"></a> Importar feeds de dados de Relatórios do Reporting Services  
 Se você tiver uma implantação do [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] Reporting Services, poderá usar a extensão de renderização Atom para gerar um feed de dados a partir de um relatório existente.  
  
#### <a name="to-import-report-data-from-a-published-reporting-services-report"></a>Para importar dados de relatórios de um relatório publicado do Reporting Services  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], clique no menu **Modelo** e em **Importar de Fonte de Dados**.  
  
2.  Na página **Conectar com uma fonte de dados** , em **Feeds de Dados**, selecione **Relatório**e clique em **Avançar**.  
  
3.  Na página Conectar a um Relatório do Microsoft SQL Server Reporting Services, em Nome de conexão amigável, digite um nome descritivo para o feed que você está acessando. Se você estiver importando vários fontes de dados, o uso de nomes descritivos para a conexão poderá ajudá-lo a lembrar como a conexão é usada.  
  
4.  Clique em **Procurar** e selecione um servidor de relatório.  
  
     Se você usar relatórios regularmente em um servidor de relatório, talvez o servidor seja listado em **Sites e Servidores Recentes**. Caso contrário, em Nome, digite um endereço para um servidor de relatório e clique em **Abrir** para procurar as pastas no site de servidor de relatório. Um exemplo de endereço para um servidor de relatório pode ser http://\<computername > / reportserver.  
  
5.  Selecione o relatório e clique em **Abrir**. Se desejar, você pode colar um link para o relatório, incluindo o caminho completo e nome do relatório, na caixa de texto **Nome** . O Assistente de Importação de Tabela conecta-se ao relatório e o processa na área de visualização.  
  
     Se o relatório usar parâmetros, você deverá especificar um parâmetro ou não será possível criar a conexão do relatório. Quando você faz isso, apenas as linhas relacionadas ao valor de parâmetro são importadas no feed de dados.  
  
    1.  Escolha um parâmetro usando a caixa de listagem ou a caixa de combinação fornecida no relatório.  
  
    2.  Clique em **Exibir Relatório** para atualizar os dados.  
  
        > [!NOTE]  
        >  A exibição do relatório salva os parâmetros selecionados com a definição do feed de dados.  
  
     Opcionalmente, clique em **Avançado** para definir propriedades específicas de provedor para o relatório.  
  
6.  Clique em **Testar Conexão** para ter certeza de que o relatório está disponível como um feed de dados. Se desejar, você também pode clicar em **Avançado** para confirmar que a propriedade **Documento de Serviço Embutido** contém XML inserido que especifica a conexão de feed de dados.  
  
7.  Clique em **Avançar** para continuar a importação.  
  
8.  Na página **Informações sobre Representação** , especifique as credenciais que o Analysis Services usará para se conectar à fonte de dados ao atualizar os dados e clique em **Avançar**.  
  
9. Na página **Selecionar Tabelas e Exibições** do assistente, marque a caixa de seleção ao lado das partes de relatório que você deseja importar como dados.  
  
     Alguns relatórios podem conter várias partes, inclusive tabelas, listas ou gráficos.  
  
10. Na caixa **Nome Amigável** , digite o nome da tabela onde você deseja salvar o feed de dados no modelo.  
  
     O nome do controle do Reporting Service será usado por padrão se nenhum nome tiver sido atribuído: por exemplo, Tablix1, Tablix2. Recomendamos que você altere esse nome durante a importação para que seja possível identificar mais facilmente a origem do feed de dados importado.  
  
11. Clique em **Visualizar e Filtro** para examinar os dados e alterar as seleções de coluna. Não é possível restringir as linhas importadas no feed de dados de relatório, mas é possível remover colunas desmarcando as caixas de seleção. Clique em **OK**.  
  
12. Na página **Selecionar Tabelas e Exibições** , clique em **Concluir**.  
  
## <a name="see-also"></a>Consulte também  
 [Fontes de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-sources-supported-ssas-tabular.md)   
 [Tipos de dados com suporte &#40;SSAS de Tabela&#41;](tabular-models/data-types-supported-ssas-tabular.md)   
 [Representação &#40;SSAS tabular&#41;](tabular-models/impersonation-ssas-tabular.md)   
 [Processar dados &#40;SSAS de Tabela&#41;](process-data-ssas-tabular.md)   
 [Importar dados &#40;SSAS de Tabela&#41;](import-data-ssas-tabular.md)  
  
  
