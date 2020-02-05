---
title: Origem ODBC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.odbcsource.f1
- sql13.ssis.designer.odbcsource.connection.f1
- sql13.ssis.designer.odbcsource.columns.f1
- sql13.ssis.designer.odbcsource.errorhandling.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 19a234b8c2939730a6c5a815885606dac15d0a0a
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "71298166"
---
# <a name="odbc-source"></a>Origem ODBC

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A origem ODBC extrai dados de um banco de dados com suporte do ODBC usando uma tabela de banco de dados, uma exibição ou uma instrução SQL.  
  
 A origem ODBC tem os seguintes modos de acesso a dados para extrair dados:  
  
-   Uma tabela ou exibição.  
  
-   Os resultados de uma instrução SQL.  
  
 A origem usa um gerenciador de conexões ODBC que especifica o provedor a ser usado.  
  
 Uma origem ODBC inclui as colunas de saída dos dados de origem. Quando colunas de saída são mapeadas no destino ODBC para as colunas de destino, poderão ocorrer erros se nenhuma coluna de saída for mapeada para as colunas de destino. Colunas de tipos diferentes podem ser mapeadas, porém se os dados de saída não forem compatíveis com o destino, um erro ocorrerá em runtime. Dependendo da configuração de comportamento do erro, o erro será ignorado, causará uma falha ou a linha será enviada à saída de erro.  
  
 A origem ODBC tem uma saída regular e uma saída de erro.  
  
## <a name="error-handling"></a>Tratamento de erros  
 A origem ODBC tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: o número que corresponde ao erro atual. Consulte a documentação do banco de dados com suporte do ODBC que você está usando para obter uma lista de erros. Para obter uma lista dos códigos de erro SSIS, consulte a Referência de código e mensagem de erro SSIS.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   As colunas de dados de saída padrão.  
  
 Dependendo da configuração de comportamento de erro, a origem ODBC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro. Para obter mais informações, consulte [Editor do Destino ODBC &#40;Página Gerenciador de Conexões&#41;](../../integration-services/data-flow/odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 Para obter informações sobre os tipos de dados com suporte da fonte ODBC, consulte Conector para ODBC.  
  
## <a name="extract-options"></a>Extrair opções  
 A origem ODBC opera no modo **Lote** ou **Linha a Linha** . O modo usado é determinado pela propriedade **FetchMethod** . A lista seguinte descreve os modos.  
  
-   **Lote**: o componente tenta usar o método de busca mais eficiente com base no provedor ODBC percebido. Para a maioria dos provedores ODBC modernos, esse é SQLFetchScroll com associação de matriz (em que o tamanho da matriz é determinado pela propriedade **BatchSize** ). Se você selecionar **Lote** e o provedor não oferecer suporte a esse método, o destino ODBC alternará automaticamente para modo **Linha a linha** .  
  
-   **Linha a linha**: o componente usa SQLFetch para recuperar as linhas uma de cada vez.  
  
 Para obter mais informações sobre a propriedade **FetchMethod** , consulte [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Paralelismo  
 Não há nenhuma limitação no número de componentes de origem ODBC que podem ser executados em paralelo na mesma tabela ou tabelas diferentes, na mesma máquina ou em máquinas diferentes (diferente de limites de sessão globais normais).  
  
 No entanto, as imitações do provedor ODBC sendo usado podem restringir o número de conexões simultâneas pelo provedor. Essas limitações restringem o número de instâncias paralelas com suporte possível para a fonte ODBC. O desenvolvedor SSIS deve estar consciente das limitações de qualquer provedor ODBC usado e considerá-las ao compilar pacotes SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Solucionando problemas da origem ODBC  
 Você pode registrar as chamadas que a origem ODBC faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem ODBC executa. Para registrar em log as chamadas que a origem ODBC faz a provedores de dados externos, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados.*  
  
## <a name="configuring-the-odbc-source"></a>Configurando a origem ODBC  
 Você pode configurar a origem ODBC programaticamente ou por meio do SSIS Designer.  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse na origem ODBC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, consulte [ODBC Source Custom Properties](../../integration-services/data-flow/odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Extrair dados por meio da origem ODBC](../../integration-services/data-flow/extract-data-by-using-the-odbc-source.md)  
  
-   [Propriedades personalizadas da origem ODBC](../../integration-services/data-flow/odbc-source-custom-properties.md)  
  
## <a name="odbc-source-editor-connection-manager-page"></a>Editor de Origem ODBC (página Gerenciador de Conexões)
  Use a página **Gerenciador de Conexões** da caixa de diálogo **Editor de Origem ODBC** para selecionar o gerenciador de conexões ODBC para a origem. Essa página também permite que você selecione uma tabela ou exibição a partir do banco de dados.  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página do Gerenciador de Conexões do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
### <a name="options"></a>Opções  
  
#### <a name="connection-manager"></a>Gerenciador de conexões  
 Selecione na lista um gerenciador de conexões ODBC existente ou clique em **Novo** para criar uma nova conexão. A conexão pode ser com qualquer banco de dados com suporte ODBC.  
  
#### <a name="new"></a>Novo  
 Clique em **Nova**. É aberta a caixa de diálogo **Configurar Editor do Gerenciador de Conexões ODBC** , na qual você pode criar um novo gerenciador de conexões ODBC.  
  
#### <a name="data-access-mode"></a>Modo de acesso a dados  
 Especifique o método para selecionar dados da origem. As opções são mostradas na tabela a seguir:  
  
|Opção|DESCRIÇÃO|  
|------------|-----------------|  
|Nome da tabela|Recupere os dados de uma tabela ou exibição na fonte de dados ODBC. Quando você selecionar esta opção, selecione um valor na lista para o seguinte:|  
||**Nome da tabela ou exibição**: selecione uma tabela ou exibição disponível na lista ou digite uma expressão regular para identificar a tabela.|  
||Essa lista contém apenas as primeiras 1.000 tabelas. Se o banco de dados contiver mais de 1.000 tabelas, você poderá digitar o início do nome de uma tabela ou usar o curinga (*) para inserir qualquer parte do nome para exibir a tabela ou tabelas desejadas.|  
|Comando SQL|Recupere os dados da fonte de dados ODBC usando uma consulta SQL. Você deve escrever a consulta na sintaxe do banco de dados de origem com o qual está trabalhando. Quando selecionar esta opção, insira uma consulta de uma das seguintes maneiras:|  
||Insira o texto da consulta SQL no campo **Texto do comando do SQL** .|  
||Clique em **Procurar** para carregar a consulta SQL de um arquivo de texto.|  
||Clique em **Analisar consulta** para verificar a sintaxe do texto da consulta.|  
  
#### <a name="preview"></a>Visualização  
 Clique em **Visualizar** para exibir até as primeiras 200 linhas dos dados extraídos da tabela ou exibição selecionada.  
  
## <a name="odbc-source-editor-columns-page"></a>Editor de Origem ODBC (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem ODBC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem ODBC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
3.  No **Editor de Origem ODBC**, clique em **Colunas**.  
  
### <a name="options"></a>Opções  
  
#### <a name="available-external-columns"></a>Colunas Externas Disponíveis  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecionar as colunas a serem usadas da origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 Marque essa caixa de seleção **Selecionar Tudo** para selecionar todas as colunas.  
  
#### <a name="external-column"></a>Coluna Externa  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem ODBC.  
  
#### <a name="output-column"></a>Coluna de Saída  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## <a name="odbc-source-editor-error-output-page"></a>Editor de Origem ODBC (página Saída de Erro)
  Use a página **Saída de Erro** da caixa de diálogo **Editor de Origem ODBC** para selecionar as opções para tratamento de erros.  
  
### <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Saída de Erro do Editor de Origem ODBC**  
  
-   No [!INCLUDE[ssBIDevStudio](../../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
-   Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
-   No **Editor de Origem ODBC**, clique em **Saída de Erro**.  
  
### <a name="options"></a>Opções  
  
#### <a name="inputoutput"></a>Entrada/Saída  
 Exibe o nome da fonte de dados.  
  
#### <a name="column"></a>Coluna  
 Não usado.  
  
#### <a name="error"></a>Erro  
 Selecione como a origem ODBC deve tratar erros em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
#### <a name="truncation"></a>Truncation  
 Selecione como a origem ODBC deve tratar o truncamento em um fluxo: ignorar a falha, redirecionar a linha ou causar falha no componente.  
  
#### <a name="description"></a>DESCRIÇÃO  
 Não usado.  
  
#### <a name="set-this-value-to-selected-cells"></a>Definir este valor para células selecionadas  
 Selecione como a origem ODBC trata todas as células selecionadas quando ocorre um erro ou um truncamento: ignorar a falha, redirecionar a linha ou causar a falha no componente.  
  
#### <a name="apply"></a>Aplicar  
 Aplique as opções de tratamento de erros às células selecionadas.  
  
### <a name="error-handling-options"></a>Opções de tratamento de erros  
 Você usa as opções a seguir para configurar como a origem ODBC trata erros e truncamentos.  
  
#### <a name="fail-component"></a>Falha no Componente  
 A tarefa Fluxo de Dados falha quando ocorre um erro ou um truncamento. Esse é o comportamento padrão.  
  
#### <a name="ignore-failure"></a>Ignorar Falha  
 O erro ou o truncamento é ignorado.  
  
#### <a name="redirect-flow"></a>Redirecionar fluxo  
 A linha que está causando o erro ou o truncamento é direcionada para a saída do erro da origem ODBC.  
  
  
