---
title: Destino ODBC | Microsoft Docs
ms.custom: 
ms.date: 03/01/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: data-flow
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.ssis.designer.odbcdest.f1
- sql13.ssis.designer.odbcdest.connection.f1
- sql13.ssis.designer.odbcdest.columns.f1
- sql13.ssis.designer.odbcdest.errorhandling.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: 
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: 34e524470a56b62657f231a22639fc3e2c20e2d1
ms.sourcegitcommit: 7519508d97f095afe3c1cd85cf09a13c9eed345f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/15/2018
---
# <a name="odbc-destination"></a>Destino ODBC
  O destino ODBC carrega dados em massa em tabelas de bancos de dados com suporte ODBC. O destino ODBC usa um gerenciador de conexões ODBC para se conectar à fonte de dados.  
  
 Um destino ODBC inclui mapeamentos entre as colunas de entrada e as colunas da fonte de dados de destino. Você não precisa mapear as colunas de entrada para todas as colunas de destino, mas, dependendo das propriedades das colunas de destino, poderão ocorrer erros se nenhuma das colunas de entrada for mapeada para as colunas de destino. Por exemplo, se uma coluna de destino não permitir valores nulos, uma coluna de entrada deve ser mapeada para aquela coluna de destino. Além disso, colunas de tipos diferentes podem ser mapeadas, porém se os dados de entrada não forem compatíveis com o tipo de coluna de destino, um erro ocorrerá em tempo de execução. Dependendo da configuração de comportamento do erro, o erro será ignorado, causará uma falha ou a linha será enviada à saída de erro.  
  
 O destino ODBC tem uma saída regular e uma saída de erro.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Opções de carregamento  
 O destino ODBC pode usar um de dois módulos de carga de acesso. Defina o modo no [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-source-editor-connection-manager-page.md). Os dois modos são:  
  
-   **Lote**: nesse modo, o destino ODBC tenta usar o método de inserção mais eficiente com base nos recursos do provedor ODBC percebido. Para a maioria dos provedores ODBC modernos, isso significa preparar uma instrução INSERT com parâmetros e usar uma associação de parâmetro de matriz row-wise (em que o tamanho da matriz é controlado pela propriedade **BatchSize** ). Se você selecionar **Lote** e o provedor não oferecer suporte a esse método, o destino ODBC alternará automaticamente para modo **Linha a linha** .  
  
-   **Linha a Linha**: nesse modo, o destino ODBC prepara uma instrução INSERT com parâmetros e usa **SQL Execute** para inserir linhas uma de cada vez.  
  
## <a name="error-handling"></a>Tratamento de erros  
 O destino ODBC tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: o número que corresponde ao erro atual. Consulte a documentação do seu banco de dados de origem para obter uma lista de erros. Para obter uma lista dos códigos de erro SSIS, consulte a Referência de código e mensagem de erro SSIS.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   As colunas de dados de saída padrão.  
  
 Dependendo da configuração de comportamento de erro, o destino ODBC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro. Para obter mais informações, consulte [Editor de origem ODBC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Paralelismo  
 Não há nenhuma limitação no número de componentes de destino ODBC que podem ser executados em paralelo na mesma tabela ou tabelas diferentes, na mesma máquina ou em máquinas diferentes (diferente de limites de sessão globais normais).  
  
 No entanto, as imitações do provedor ODBC sendo usado podem restringir o número de conexões simultâneas pelo provedor. Essas limitações restringem o número de instâncias paralelas com suporte possível para o destino ODBC. O desenvolvedor SSIS deve estar consciente das limitações de qualquer provedor ODBC usado e considerá-las ao compilar pacotes SSIS.  
  
 Você também deve estar ciente de que i carregamento simultâneo na mesma tabela pode reduzir o desempenho devido ao bloqueio de registro padrão. Isso depende dos dados sendo carregados e da organização da tabela.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Solucionando problemas do destino ODBC  
 Você pode registrar as chamadas que a origem ODBC faz para provedores de dados externos. É possível usar essa capacidade de registro para solucionar o problema de salvar os dados em fontes de dados externas que o destino ODBC executa. Para registrar em log as chamadas que o destino ODBC faz a provedores de dados externos, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados*.  
  
## <a name="configuring-the-odbc-destination"></a>Configurando o destino ODBC  
 Você pode configurar o destino ODBC programaticamente ou por meio do SSIS Designer  
  
 Para obter mais informações, consulte um dos tópicos a seguir.  
  
-   [Editor do Destino ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md)  
  
-   [Editor de Destinos ODBC &#40;Página Mapeamentos&#41;](../../integration-services/data-flow/odbc-destination-editor-mappings-page.md)  
  
-   [Editor do Destino ODBC &#40;Página Saída de Erro&#41;](../../integration-services/data-flow/odbc-destination-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse no destino ODBC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, consulte [Propriedades personalizadas de destino ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Carregar dados por meio do destino ODBC](../../integration-services/data-flow/load-data-by-using-the-odbc-destination.md)  
  
-   [Propriedades personalizadas de destino ODBC](../../integration-services/data-flow/odbc-destination-custom-properties.md)  
  
## <a name="odbc-destination-editor-connection-manager-page"></a>Editor do Destino ODBC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Destino ODBC** para selecionar o gerenciador de conexões para o destino. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados  
  
 **Para abrir a página do Gerenciador de Conexões do Editor de Destino ODBC**  
  
### <a name="task-list"></a>Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Gerenciador de Conexões**.  
  
### <a name="options"></a>Opções  
  
#### <a name="connection-manager"></a>Gerenciador de conexões  
 Selecione na lista um gerenciador de conexões ODBC existente ou clique em Novo para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
#### <a name="new"></a>Nova  
 Clique em **Nova**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões.  
  
#### <a name="data-access-mode"></a>Modo de acesso a dados  
 Selecione o método de carregamento de dados no destino. As opções são mostradas na tabela a seguir:  
  
|Opção|Description|  
|------------|-----------------|  
|Nome da Tabela - Lote|Selecione esta opção para configurar o destino ODBC para trabalhar no modo de lote. Ao selecionar esta opção, as seguintes opções estão disponíveis:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (\*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.<br /><br /> **Tamanho do lote**: digite o tamanho do lote para carregamento em massa. Esse é o número de linhas carregadas como um lote|  
|Nome da Tabela - Linha a Linha|Selecione esta opção para configurar o destino ODBC para inserir cada uma das linhas na tabela de destino, uma de cada vez. Ao selecionar esta opção, a seguinte opção está disponível:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível no banco de dados na lista.<br /><br /> Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
  
#### <a name="preview"></a>Visualização  
 Clique em **Visualizar** para exibir até 200 linhas de dados da tabela selecionada.  
  
## <a name="odbc-destination-editor-mappings-page"></a>Editor de Destino ODBC (página Mapeamentos)
  Use a página **Mapeamentos** da caixa de diálogo **ODBC Destination Editor (Editor de Destino ODBC)** para mapear colunas de entrada para colunas de destino.  
  
### <a name="options"></a>Opções  
  
#### <a name="available-input-columns"></a>Colunas de Entrada Disponíveis  
 A lista de colunas de entrada disponíveis. Arraste e solte uma coluna de entrada em uma coluna de destino disponível para mapear as colunas.  
  
#### <a name="available-destination-columns"></a>Colunas de Destino Disponíveis  
 A lista de colunas de destino disponíveis. Arraste e solte uma coluna de destino em uma coluna de entrada disponível para mapear as colunas.  
  
#### <a name="input-column"></a>Coluna de Entrada  
 Exiba as colunas de entrada que você selecionou. Você pode remover mapeamentos selecionando **\<ignorar>** para excluir colunas da saída.  
  
#### <a name="destination-column"></a>Coluna de Destino  
 Exiba todas as colunas de destino disponíveis, mapeadas e não mapeadas.  
  
## <a name="odbc-destination-editor-error-output-page"></a>Editor de Destinos ADO NET (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Destino ODBC** para selecionar as opções para tratamento de erros.  
  
 **Para abrir a página Saída de Erro do Editor de Destino ODBC**  
  
### <a name="task-list"></a>Lista de Tarefas  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem o destino ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes no destino ODBC.  
  
-   No **Editor de Destino ODBC**, clique em **Saída de Erro**.  
  
### <a name="options"></a>Opções  
  
#### <a name="inputoutput"></a>Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
#### <a name="column"></a>coluna  
 Não usado.  
  
#### <a name="error"></a>Erro  
 Selecione como o destino ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
#### <a name="truncation"></a>Truncation  
 Selecione como o destino ODBC deve tratar truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
#### <a name="description"></a>Description  
 Exiba uma descrição do erro.  
  
#### <a name="set-this-value-to-selected-cells"></a>Definir este valor para células selecionadas  
 Selecione como o destino ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
#### <a name="apply"></a>Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
### <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como o destino ODBC trata erros e truncamentos.  
  
#### <a name="fail-component"></a>Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
#### <a name="ignore-failure"></a>Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
#### <a name="redirect-flow"></a>Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro do destino ODBC. Para obter mais informações, consulte Destino ODBC.  
  
