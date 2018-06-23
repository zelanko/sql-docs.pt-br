---
title: Destino ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.ssis.designer.odbcdest.f1
ms.assetid: bffa63e0-c737-4b54-b4ea-495a400ffcf8
caps.latest.revision: 11
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 648e743d67b308e7dae75106165d65183fd735c8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36006163"
---
# <a name="odbc-destination"></a>Destino ODBC
  O destino ODBC carrega dados em massa em tabelas de bancos de dados com suporte ODBC. O destino ODBC usa um gerenciador de conexões ODBC para se conectar à fonte de dados.  
  
 Um destino ODBC inclui mapeamentos entre as colunas de entrada e as colunas da fonte de dados de destino. Você não precisa mapear as colunas de entrada para todas as colunas de destino, mas, dependendo das propriedades das colunas de destino, poderão ocorrer erros se nenhuma das colunas de entrada for mapeada para as colunas de destino. Por exemplo, se uma coluna de destino não permitir valores nulos, uma coluna de entrada deve ser mapeada para aquela coluna de destino. Além disso, colunas de tipos diferentes podem ser mapeadas, porém se os dados de entrada não forem compatíveis com o tipo de coluna de destino, um erro ocorrerá em tempo de execução. Dependendo da configuração de comportamento do erro, o erro será ignorado, causará uma falha ou a linha será enviada à saída de erro.  
  
 O destino ODBC tem uma saída regular e uma saída de erro.  
  
##  <a name="BKMK_odbcdestination_loadoptions"></a> Opções de carregamento  
 O destino ODBC pode usar um de dois módulos de carga de acesso. Defina o modo no [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../odbc-source-editor-connection-manager-page.md). Os dois modos são:  
  
-   **Lote**: nesse modo, o destino ODBC tenta usar o método de inserção mais eficiente com base nos recursos do provedor ODBC percebido. Para a maioria dos provedores ODBC modernos, isso significa preparar uma instrução INSERT com parâmetros e usar uma associação de parâmetro de matriz row-wise (em que o tamanho da matriz é controlado pela propriedade **BatchSize** ). Se você selecionar **Lote** e o provedor não oferecer suporte a esse método, o destino ODBC alternará automaticamente para modo **Linha a linha** .  
  
-   **Linha a Linha**: nesse modo, o destino ODBC prepara uma instrução INSERT com parâmetros e usa **SQL Execute** para inserir linhas uma de cada vez.  
  
## <a name="error-handling"></a>Tratamento de erros  
 O destino ODBC tem uma saída de erro. A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: o número que corresponde ao erro atual. Consulte a documentação do seu banco de dados de origem para obter uma lista de erros. Para obter uma lista dos códigos de erro SSIS, consulte a Referência de código e mensagem de erro SSIS.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   As colunas de dados de saída padrão.  
  
 Dependendo da configuração de comportamento de erro, o destino ODBC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro. Para obter mais informações, consulte [Editor de origem ODBC &#40;Página Saída de Erro&#41;](../odbc-source-editor-error-output-page.md).  
  
## <a name="parallelism"></a>Paralelismo  
 Não há nenhuma limitação no número de componentes de destino ODBC que podem ser executados em paralelo na mesma tabela ou tabelas diferentes, na mesma máquina ou em máquinas diferentes (diferente de limites de sessão globais normais).  
  
 No entanto, as imitações do provedor ODBC sendo usado podem restringir o número de conexões simultâneas pelo provedor. Essas limitações restringem o número de instâncias paralelas com suporte possível para o destino ODBC. O desenvolvedor SSIS deve estar consciente das limitações de qualquer provedor ODBC usado e considerá-las ao compilar pacotes SSIS.  
  
 Você também deve estar ciente de que i carregamento simultâneo na mesma tabela pode reduzir o desempenho devido ao bloqueio de registro padrão. Isso depende dos dados sendo carregados e da organização da tabela.  
  
## <a name="troubleshooting-the-odbc-destination"></a>Solucionando problemas do destino ODBC  
 Você pode registrar as chamadas que a origem ODBC faz para provedores de dados externos. É possível usar essa capacidade de registro para solucionar o problema de salvar os dados em fontes de dados externas que o destino ODBC executa. Para registrar em log as chamadas que o destino ODBC faz a provedores de dados externos, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados*.  
  
## <a name="configuring-the-odbc-destination"></a>Configurando o destino ODBC  
 Você pode configurar o destino ODBC programaticamente ou por meio do SSIS Designer  
  
 Para obter mais informações, consulte um dos tópicos a seguir.  
  
-   [Editor de destino ODBC &#40;página Gerenciador de Conexão&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [Editor de destino ODBC &#40;página mapeamentos&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor de destino ODBC &#40;página de saída de erro&#41;](../odbc-destination-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse no destino ODBC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, consulte [Propriedades personalizadas de destino ODBC](odbc-destination-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Editor de destino ODBC &#40;página de saída de erro&#41;](../odbc-destination-editor-error-output-page.md)  
  
-   [Editor de destino ODBC &#40;página mapeamentos&#41;](../odbc-destination-editor-mappings-page.md)  
  
-   [Editor de destino ODBC &#40;página Gerenciador de Conexão&#41;](../odbc-destination-editor-connection-manager-page.md)  
  
-   [Carregar dados por meio do destino ODBC](odbc-destination.md)  
  
-   [Propriedades personalizadas de destino ODBC](odbc-destination-custom-properties.md)  
  
  