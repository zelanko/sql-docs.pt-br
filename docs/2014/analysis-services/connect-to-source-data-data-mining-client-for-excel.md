---
title: Conectar-se a dados de origem (cliente de mineração de dados para Excel) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- connections
ms.assetid: 548672ce-e403-4aca-b67a-c2c797f053dd
author: minewiskan
ms.author: owend
ms.openlocfilehash: 8c90031f3c1191e99ff6274f6198d513225f0927
ms.sourcegitcommit: 2f166e139f637d6edfb5731510d632a13205eb25
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/08/2020
ms.locfileid: "84527012"
---
# <a name="connect-to-source-data-data-mining-client-for-excel"></a>Conectar a dados de origem (Cliente de Mineração de Dados para Excel)
  Este tópico descreve como criar e usar as conexões usadas para armazenar modelos de mineração de dados e para acessar os dados externos armazenados no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Conexões de mineração de dados.** A conexão inicial criada quando você inicia os suplementos é usada para acessar algoritmos, analisar dados e armazenar a estrutura e os modelos de mineração.  
  
 Uma conexão para uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] é necessária para usar as ferramentas de modelagem e visualização, porque os suplementos dependem de algoritmos e estruturas de dados fornecidos pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
 **Conexões para fontes de dados externas.** Você também pode criar conexões com dados externos quando estiver criando modelos ou salvando os resultados. Por exemplo, você pode criar um modelo de mineração de dados em um servidor e, em seguida, executar uma consulta de previsão em relação ao modelo de mineração de dados usando dados armazenados em outra instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], em uma tabela de dados do Excel ou em uma fonte de dados externa, como o [!INCLUDE[msCoName](../includes/msconame-md.md)] Access. Cada vez que você acessar uma nova fonte de dados, receberá uma solicitação para criar uma conexão usando uma caixa de diálogo.  
  
##  <a name="prerequisites"></a><a name="bkmk_prereq2"></a> Pré-requisitos  
 Esta versão dos suplementos requer que sua instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] seja SQL Server 2012. Uma versão separada dos suplementos estará disponível se você quiser se conectar a uma versão anterior do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Há versões dos suplementos que oferecem suporte ao SQL Server 2005, ao SQL Server 2008 e ao SQL Server 2008 R2.  
  
 Para se conectar a um banco de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], você deve ter permissões para acessar o servidor do banco de dados. Além disso, as sessões de mineração de dados devem ser habilitadas e você deve ter permissões de leitura ou leitura/gravação nos objetos de banco de dados armazenados no servidor.  
  
##  <a name="creating-data-mining-server-connections"></a><a name="bkmk_connect"></a>Criando conexões do servidor de mineração de dados  
 O grupo de **conexões** no cliente de mineração de dados para Excel e as ferramentas de análise de tabela para Excel fornecem ferramentas para gerenciar conexões com uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
-   Você pode criar a conexão quando instala o suplemento ou pode adicionar uma conexão depois.  
  
-   Você pode criar várias conexões e alterar conexões a qualquer momento, a menos que esteja no processo de criar ou consultar um modelo.  
  
     Não altere nem feche uma conexão quando um modelo de mineração de dados estiver sendo processado. O modelo de mineração de dados pode perder dados ou se tornar inutilizável.  
  
-   Apenas uma conexão pode estar ativa em um determinado momento.  
  
### <a name="connections-in-the-excel-add-ins"></a>Conexões nos suplementos do Excel  
 O grupo de **conexões** no cliente de mineração de dados para Excel e as ferramentas de análise de tabela para Excel são onde você gerencia conexões com uma instância do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] .  
  
##### <a name="create-a-new-server-connection-in-the-excel-add-ins"></a>Criar uma nova conexão de servidor nos suplementos do Excel  
  
1.  Clique no botão **conexão** na faixa de medida **analisar** ou **mineração de dados** .  
  
    > [!NOTE]  
    >  O texto do botão indica se uma conexão existe. Quando nenhuma conexão foi feita na planilha, o botão contém o texto " \<No connection> ." Se uma conexão tiver sido feita anteriormente na pasta de trabalho, o nome dessa conexão aparecerá no botão.  
  
2.  Na caixa de diálogo **Analysis Services conexões** , clique em **novo**.  
  
3.  Na caixa de diálogo **nova conexão Analysis Services** , digite o nome do servidor.  
  
4.  Especifique o método de autenticação.  
  
5.  Selecione um banco de dados na lista suspensa **nome do catálogo** . Se não existir nenhum banco de dados na instância, selecione **(padrão)**.  
  
6.  Digite um nome amigável para a conexão.  
  
7.  Clique em **testar conexão** para verificar se o servidor e o banco de dados estão disponíveis.  
  
8.  Clique em **OK** e em **Fechar**.  
  
### <a name="connections-using-a-web-service"></a>Conexões usando um serviço Web  
 Se você estiver usando uma arquitetura de cliente fino para habilitar a procura de cubos e dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], também poderá configurar uma conexão com um servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] por meio de serviços Web. Para obter informações sobre como definir um cliente com base na Web, consulte os Manuais Online do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)].  
  
 Se você tiver acesso a um servidor que tenha sido configurado para serviços Web, especifique o tipo de conexão ao criá-la.  
  
##### <a name="create-an-http-connection-to-analysis-services"></a>Criar uma conexão HTTP com o Analysis Services  
  
1.  Abra a caixa de diálogo **nova conexão Analysis Services** .  
  
2.  Para o nome do servidor, digite http:// seguido pela URL atribuída ao servidor [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)].  
  
3.  Digite o nome de usuário e a senha necessários para acessar o serviço Web.  
  
### <a name="connections-in-the-visio-add-in"></a>Conexões no suplemento do Visio  
 Diferente do Excel, o Visio não fornece uma faixa de opções de ferramentas e não há botões especificamente para criar ou monitorar conexões. Em vez disso, a conexão de dados é criada quando você seleciona pela primeira vez uma forma de mineração de dados solta-a em uma página do Visio. Um assistente solicitará que você selecione o modelo para a forma e defina outras opções.  
  
 Caso você tenha usado anteriormente uma conexão com uma fonte de dados do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] no Excel, essas conexões serão listadas como possíveis fontes de dados para selecionar.  
  
##### <a name="create-a-connection-for-a-visio-shape"></a>Criar uma conexão de dados para uma forma do Visio  
  
1.  Abra o Modelo de Mineração de Dados e selecione uma das formas de mineração de dados.  
  
2.  Arraste e solte a forma para uma página em branco.  
  
3.  Na caixa de diálogo **selecionar uma fonte de dados** , selecione uma fonte de dados na lista ou clique em **novo**.  
  
4.  Se você selecionar **novo**, siga o procedimento descrito anteriormente para especificar um nome de servidor e catálogo, ou para se conectar por meio de um serviço Web.  
  
##  <a name="changing-connections"></a><a name="bkmk_change"></a>Alterando conexões  
 Você pode criar várias conexões na mesma planilha, mas somente uma conexão pode ficar ativa de cada vez. O nome da conexão atual é exibido no botão **conexão** .  
  
 No cliente de mineração de dados para Excel, você também pode verificar a cadeia de conexão e o status da conexão atual clicando em **rastrear** e, em seguida, clicando em **conexão atual**.  
  
#### <a name="use-a-different-server-connection"></a>Usar uma conexão de servidor diferente  
  
1.  Clique em **conexão**.  
  
2.  No painel **conexões Analysis Services** , selecione uma conexão na lista **outras conexões** e clique em **tornar atual**.  
  
3.  Clique em **testar conexão** para verificar se a conexão está disponível.  
  
 Após a conclusão do processamento de um modelo de mineração, os resultados serão armazenados localmente, e não haverá efeito sobre os dados se você fechar a conexão com um servidor e se conectar a outro servidor. No entanto, evite alterar as conexões ou perder a conexão quando um modelo de mineração de dados estiver sendo processado, porque isso pode corromper os dados.  
  
#### <a name="modify-an-existing-server-connection"></a>Modifique uma conexão de servidor existente  
  
1.  Você não pode alterar uma conexão existente; se quiser se conectar a um banco de dados diferente ou a um servidor diferente, deverá criar uma nova conexão.  
  
2.  Se você precisar modificar a cadeia de conexão para aumentar o tempo limite de consulta ou adicionar outros parâmetros específicos para a sua instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)], uma opção é editar o arquivo .dmc, onde a cadeia de conexão está armazenada.  
  
     \<drive:>O \\ \> suplemento de mineração \AppData\Local\Microsoft\Data myusername<  
  
##  <a name="connecting-to-external-data-sources"></a><a name="bkmk_extconnections"></a>Conectando-se a fontes de dados externas  
 Enquanto as ferramentas na faixa de medida de **análise** funcionam exclusivamente com dados no Excel, as ferramentas na faixa de informações de **mineração de dados** permitem que você se conecte diretamente a fontes de dados externas para usar como entradas para seu modelo ou para amostragem.  
  
 As ferramentas a seguir nesses suplementos dão suporte ao uso de dados externos para mineração de dados:  
  
-   [&#40;de dados de exemplo SQL Server suplementos de mineração de dados&#41;](sample-data-sql-server-data-mining-add-ins.md)  
  
-   [Assistente de classificação &#40;suplementos de mineração de dados para Excel&#41;](classify-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Assistente de estimativa &#40;suplementos de mineração de dados para Excel&#41;](estimate-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Assistente de cluster &#40;suplementos de mineração de dados para Excel&#41;](cluster-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Assistente de previsão &#40;suplementos de mineração de dados para Excel&#41;](forecast-wizard-data-mining-add-ins-for-excel.md)  
  
-   [Crie &#40;de estrutura de mineração SQL Server suplementos de mineração de dados&#41;](create-mining-structure-sql-server-data-mining-add-ins.md)  
  
-   [Gráfico de precisão &#40;SQL Server suplementos de mineração de dados&#41;](accuracy-chart-sql-server-data-mining-add-ins.md)  
  
-   [&#40;de gráfico de ganho SQL Server suplementos de mineração de dados&#41;](profit-chart-sql-server-data-mining-add-ins.md)  
  
-   [&#40;de matrizes de classificação SQL Server suplementos de mineração de dados&#41;](classification-matrix-sql-server-data-mining-add-ins.md)  
  
### <a name="using-analysis-services-as-a-data-source"></a>Usando Analysis Services como uma fonte de dados  
 Você não pode acessar diretamente os dados armazenados em um cubo ou modelo tabular do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Em vez disso, crie uma conexão no Excel para o servidor do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] e use os dados para criar um modelo.  
  
### <a name="relational-data-sources"></a>Fontes de dados relacionais  
 Se quiser usar dados de uma fonte relacional como entrada para o modelo, você poderá se conectar às seguintes versões do SQL Server:  
  
-   SQL Server 2008  
  
-   SQL Server 2008 R2  
  
-   SQL Server 2012  
  
 Você também pode obter dados de qualquer outra fonte de dados relacional que tem suporte como uma fonte de dados pelo [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Para obter informações sobre as fontes de dados com suporte, consulte [fontes de dados em modelos multidimensionais](multidimensional-models/data-sources-in-multidimensional-models.md)  
  
 Observe que os seguintes tipos de dados não podem ser usados para mineração de dados e resultarão em um erro se forem incluídos quando você criar um modelo:  
  
-   ntext  
  
-   binary  
  
## <a name="see-also"></a>Consulte Também  
 [Rastrear &#40;cliente de mineração de dados para Excel&#41;](trace-data-mining-client-for-excel.md)  
  
  
