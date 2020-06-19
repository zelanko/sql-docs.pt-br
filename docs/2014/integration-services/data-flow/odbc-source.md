---
title: Origem ODBC | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.f1
ms.assetid: abcf34eb-9140-4100-82e6-b85bccd22abe
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 2f7d241a8cfb7386e58dfa490bf66ef463613de6
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84915006"
---
# <a name="odbc-source"></a>Origem ODBC
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
  
 Dependendo da configuração de comportamento de erro, a origem ODBC oferece suporte ao retorno de erros (conversão de dados, truncamento) que ocorre durante o processo de extração na saída de erro. Para obter mais informações, consulte [Editor do Destino ODBC &#40;Página Gerenciador de Conexões&#41;](../odbc-destination-editor-connection-manager-page.md).  
  
## <a name="data-type-support"></a>Suporte do tipo de dados  
 Para obter informações sobre os tipos de dados com suporte da origem ODBC, consulte Conector para ODBC da Attunity.  
  
## <a name="extract-options"></a>Extrair opções  
 A origem ODBC opera no modo **Lote** ou **Linha a Linha** . O modo usado é determinado pela propriedade **FetchMethod** . A lista seguinte descreve os modos.  
  
-   **Lote**: o componente tenta usar o método de busca mais eficiente com base no provedor ODBC percebido. Para a maioria dos provedores ODBC modernos, esse é SQLFetchScroll com associação de matriz (em que o tamanho da matriz é determinado pela propriedade **BatchSize** ). Se você selecionar **Lote** e o provedor não oferecer suporte a esse método, o destino ODBC alternará automaticamente para modo **Linha a linha** .  
  
-   **Linha a linha**: o componente usa SQLFetch para recuperar as linhas uma de cada vez.  
  
 Para obter mais informações sobre a propriedade **FetchMethod** , consulte [ODBC Source Custom Properties](odbc-source-custom-properties.md).  
  
## <a name="parallelism"></a>Paralelismo  
 Não há nenhuma limitação no número de componentes de origem ODBC que podem ser executados em paralelo na mesma tabela ou tabelas diferentes, na mesma máquina ou em máquinas diferentes (diferente de limites de sessão globais normais).  
  
 No entanto, as imitações do provedor ODBC sendo usado podem restringir o número de conexões simultâneas pelo provedor. Essas limitações restringem o número de instâncias paralelas com suporte possível para a fonte ODBC. O desenvolvedor SSIS deve estar consciente das limitações de qualquer provedor ODBC usado e considerá-las ao compilar pacotes SSIS.  
  
## <a name="troubleshooting-the-odbc-source"></a>Solucionando problemas da origem ODBC  
 Você pode registrar as chamadas que a origem ODBC faz para provedores de dados externos. Você pode usar essa capacidade de registro para solucionar problemas de carregamento de dados de fontes de dados externas que a origem ODBC executa. Para registrar em log as chamadas que a origem ODBC faz a provedores de dados externos, habilite o rastreamento do gerenciador de driver ODBC. Para obter mais informações, consulte a documentação da Microsoft em *Como gerar um rastreamento ODBC com o administrador de fonte de dados.*  
  
## <a name="configuring-the-odbc-source"></a>Configurando a origem ODBC  
 Você pode configurar a origem ODBC programaticamente ou por meio do SSIS Designer.  
  
 Para obter mais informações, consulte um dos tópicos a seguir.  
  
-   [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Editor de Origem ODBC &#40;Página Colunas&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../odbc-source-editor-error-output-page.md)  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse na origem ODBC e selecione **Mostrar Editor Avançado**.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas na caixa de diálogo Editor Avançado, consulte [ODBC Source Custom Properties](odbc-source-custom-properties.md).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../odbc-source-editor-error-output-page.md)  
  
-   [Editor de Origem ODBC &#40;Página Colunas&#41;](../odbc-source-editor-columns-page.md)  
  
-   [Editor de Fonte ODBC &#40;Página Gerenciador de Conexões&#41;](../odbc-source-editor-connection-manager-page.md)  
  
-   [Extrair dados por meio da origem ODBC](odbc-source.md)  
  
-   [ODBC Source Custom Properties](odbc-source-custom-properties.md)  
  
  
