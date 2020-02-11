---
title: Construtor de Relatórios no SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- "10428"
helpviewer_keywords:
- overview of Report Builder
- getting started
ms.assetid: 55bf4f9c-d037-412f-ae57-3fc39ce32fa5
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 3f03f0f4c210408324ee4a2cae255ba805e0377a
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66107706"
---
# <a name="report-builder-in-sql-server-2014"></a>Construtor de Relatórios no SQL Server 2014
  O Construtor de Relatórios é um ambiente de criação de relatório para usuários comerciais que preferem trabalhar no ambiente do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Office. Quando você cria um relatório, especifica onde obter os dados, que dados obter e como exibir os dados. Ao executar o relatório, o processador de relatório obtém todas as informações especificadas, recupera os dados e os combina ao layout de relatório para gerar o relatório. Você pode visualizar os relatórios no Construtor de Relatórios ou publicá-los em um servidor de relatório ou em um servidor de relatório no modo integrado do SharePoint, onde outras pessoas poderão executá-lo.  
  
 O relatório nesta ilustração caracteriza uma matriz com grupos de linhas e colunas, minigráficos, indicadores e um gráfico de pizza resumido na célula de canto, acompanhada de um mapa com dois conjuntos de dados geográficos representados pela cor e pelo tamanho do círculo.  
  
 ![rs_GettingStartedReport](../media/rs-gettingstartedreport.gif "rs_GettingStartedReport")  
  
##  <a name="JumpStartReptCreation"></a>Iniciar a criação de relatório  
  
-   **Inicie seu relatório withreport partes** criadas por outra pessoa na sua equipe. As partes de relatório são itens de relatório que foram publicados separadamente em um servidor de relatório ou em um site do SharePoint integrado a um servidor de relatório. Elas podem ser reutilizadas em outros relatórios. Itens de relatório como tabelas, matrizes, gráficos e imagens podem ser publicados como partes de relatório.  
  
-   **Comece com um conjunto de um DataSet compartilhado** criado por outra pessoa na sua equipe. Os conjuntos de dados compartilhados são consultas baseadas em uma fonte de dados compartilhados salvos em um servidor de relatório ou em um site do SharePoint integrado a um servidor de relatório.  
  
-   **Comece com o assistente de tabela, matriz ou gráfico**. Escolha uma conexão de fonte de dados, arraste e solte campos para criar uma consulta de conjunto de dados, selecione um layout e um estilo e personalize seu relatório.  
  
-   **Comece com o assistente de mapa** para criar relatórios que exibem dados agregados em relação a um plano de fundo geográfico ou geométrico. Os dados de mapa podem ser dados espaciais de uma consulta [!INCLUDE[tsql](../../includes/tsql-md.md)] ou um arquivo de forma ESRI (Environmental Systems Research Institute, Inc.). Também é possível adicionar um plano de fundo de peça de mapa do [!INCLUDE[msCoName](../../../includes/msconame-md.md)] Bing.  
  

  
##  <a name="DesignRept"></a>Criar seu relatório  
  
-   **Crie relatórios com tabela, matriz, gráfico e layouts de relatório de forma livre.** Crie relatórios de tabelas para dados baseados em colunas, relatórios de matriz (como relatórios de tabela de referência cruzada ou de Tabela Dinâmica) para dados resumidos, relatórios de gráficos para dados geográficos e relatórios de formato livre para qualquer outra finalidade. Os relatórios podem ser inseridos em outros relatórios e gráficos, junto com listas, gráficos e controles para aplicativos dinâmicos baseados na Web.  
  
-   **Relatório de uma variedade de fontes de dados.** Crie relatórios usando dados de qualquer tipo de fonte de dados que [!INCLUDE[msCoName](../../../includes/msconame-md.md)] [!INCLUDE[dnprdnshort](../../includes/dnprdnshort-md.md)]tenha um provedor de dados gerenciado, provedor de OLE DB ou fonte de dados ODBC. Você pode criar relatórios que usam dados relacionais e multidimensionais do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)], Oracle, Hyperion e outros bancos de dados. Você pode usar uma extensão de processamento de dados XML para recuperar dados de qualquer fonte de dados XML. Também é possível usar funções com valor de tabela para projetar fontes de dados personalizadas.  
  
-   **Modificar relatórios existentes.** Usando Construtor de Relatórios, você pode personalizar e atualizar relatórios que foram criados no [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)]Report Designer.  
  
-   **Modifique seus dados** filtrando, agrupando e classificando dados ou adicionando fórmulas ou expressões.  
  
-   **Adicione gráficos, medidores, minigráficos e indicadores** para resumir dados em um formato visual e apresentar grandes volumes de informações agregadas em um relance.  
  
-   **Adicione recursos interativos** , como mapas de documentos, botões Mostrar/ocultar e links de detalhamento a sub-relatórios e relatórios detalhados. Use parâmetros e filtros para filtrar dados para exibições personalizadas.  
  
-   **Insira ou referencie imagens** e outros recursos, incluindo conteúdo externo.  
  

  
##  <a name="ManageRpt"></a>Gerenciar seu relatório  
  
-   **Salve a definição do relatório** em seu computador ou no servidor de relatório, onde você pode gerenciá-lo e compartilhá-lo com outras pessoas.  
  
-   **Escolha um formato de apresentação** ao abrir o relatório ou depois de abrir o relatório. Você pode selecionar formatos voltados para a Web, para a página e de aplicativos de desktop. Os formatos incluem HTML, MHTML, PDF, XML, CSV, TIFF, Word e Excel.  
  
-   **Configure as assinaturas.** Depois de publicar o relatório no servidor de relatório ou em um servidor de relatório no modo integrado do SharePoint, você poderá configurá-lo para ser executado em um determinado horário, criar um histórico do relatório e configurar assinaturas de email.  
  
-   **Gere feeds de dados** do seu relatório usando a extensão de renderização Reporting Services Atom.  
  
> [!NOTE]  
>  Os relatórios publicados são gerenciados em um servidor de relatório ou um servidor de relatório no modo integrado do SharePoint por um administrador do servidor de relatório. Os administradores de servidor de relatório podem definir a segurança, estabelecer as propriedades e agendar operações, como histórico de relatório e entrega de relatório de email. Também podem criar agendas e fontes de dados compartilhadas e disponibilizá-las para uso geral. Os administradores também gerenciam todas as pastas de servidor de relatório. A possibilidade de executar tarefas de gerenciamento depende das permissões de usuário.  
  

  
##  <a name="InThisSection"></a> Nesta seção  
 [Novidades no Construtor de Relatórios para SQL Server 2014](../what-s-new-in-report-builder-for-sql-server-2014.md)  
 Descreve os novos recursos nesta versão do Construtor de Relatórios, inclusive mapas.  
  
 [Tutorial: Criando um relatório de gráfico rápido offline](tutorial-create-a-quick-chart-report-offline-report-builder.md)  
 Apresenta o Construtor de Relatórios e os assistentes disponíveis para ajudá-lo a criar relatórios. O tutorial fornece um conjunto de dados com o qual trabalhar, de modo que você não precise se conectar a uma fonte de dados para começar.  
  
 [Planejando um relatório &#40;Construtor de Relatórios&#41;](../report-design/planning-a-report-report-builder.md)  
 Fornece informações sobre o que você deve considerar antes de começar a criar seu relatório.  
  
 [Conceitos de criação de relatório &#40;Construtor de Relatórios e SSRS&#41;](../report-design/report-authoring-concepts-report-builder-and-ssrs.md)  
 Define os conceitos-chave usados em toda a documentação do Construtor de Relatórios.  
  
 [Modo de exibição de Design de relatório &#40;Construtor de Relatórios&#41;](report-design-view-report-builder.md)  
 Explica os diferentes painéis e regiões da exibição de design de relatório.  
  
 [Modo de exibição de design de conjunto de &#40;compartilhado Construtor de Relatórios&#41;](shared-dataset-design-view-report-builder.md)  
 Explica os diferentes painéis e regiões da exibição de design do conjunto de dados compartilhados.  
  
 [Atalhos de teclado &#40;Construtor de Relatórios&#41;](keyboard-shortcuts-report-builder.md)  
 Descreve as teclas de atalho disponíveis para navegar e criar relatórios no Construtor de Relatórios.  
  
 [Iniciar Construtor de Relatórios &#40;Construtor de Relatórios&#41;](start-report-builder.md)  
 Explica como iniciar as duas versões diferentes do Construtor de Relatórios: autônoma e [!INCLUDE[ndptecclick](../../includes/ndptecclick-md.md)].  
  
  
