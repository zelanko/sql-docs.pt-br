---
title: "Adicionar um relat&#243;rio novo ou existente a um projeto de relat&#243;rio (SSRS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/17/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "reporting-services-sharepoint"
  - "reporting-services-native"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "relatórios [Reporting Services], criando"
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
caps.latest.revision: 20
author: "guyinacube"
ms.author: "asaxton"
manager: "erikre"
caps.handback.revision: 19
---
# Adicionar um relat&#243;rio novo ou existente a um projeto de relat&#243;rio (SSRS)
  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode adicionar um novo relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] usando o Assistente de Relatório ou acrescentando um novo relatório em branco ao projeto. Também é possível adicionar um relatório existente. Depois de adicionar um relatório, você poderá ver o nome do relatório listado na pasta **Relatórios** do seu projeto.  
  
> [!NOTE]  
>  Para visualizar um relatório com fontes de dados existentes, é preciso ter as permissões para a fonte de dados do cliente que está criando o relatório. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Depois de adicionar um relatório, é possível definir as fontes de dados e os conjuntos de dados, e criar um layout de relatório. Para começar, consulte [Criando um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) ou [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## Para adicionar um novo relatório usando o Assistente de Relatórios  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Relatórios e clique em **Adicionar Novo Relatório**. A caixa de diálogo **Assistente de Relatório** é aberta.  
  
     O assistente conduzirá você pela criação de uma fonte de dados, a criação de um conjunto de dados com uma consulta, a definição de grupos, a escolha de um estilo que inclua cor e fonte, e a criação do relatório. As etapas incluem:  
  
    -   **Selecionar uma fonte de dados.** A primeira etapa ao criar um relatório é definir uma fonte de dados. O Assistente de Relatório apresenta uma lista de todas as fontes de dados compartilhadas no projeto de relatório, além de uma opção para criar uma nova fonte de dados.  
  
    -   **Criar uma consulta.** A próxima etapa é criar uma consulta. É possível digitar a cadeia de caracteres da consulta, gerar no Designer de Consulta ou importar uma consulta a partir de outro relatório. Para obter informações sobre Designers de Consulta, consulte [Designers de Consulta do Reporting Services](../Topic/Reporting%20Services%20Query%20Designers.md).  
  
    -   **Escolher um tipo de relatório.** A próxima etapa é selecionar o tipo de relatório desejado. Você pode optar por um relatório tabular ou de matriz. Um relatório tabular tem um número fixo de colunas. Uma relatório de matriz ou de tabulação cruzada apresenta um número variável de colunas com base nos resultados da consulta. Um relatório de mapa exibe dados analíticos em relação a um plano de fundo geográfico.  
  
    -   **Escolher um estilo.** A próxima etapa é aplicar um estilo ao relatório que usa um modelo de estilo. Selecione um modelo para aplicar estilos como fonte, cor e estilo de borda ao relatório. O Designer de Relatórios fornece seis modelos de estilo: Ardósia, Floresta, Corporativo, Negrito, Azul-marinho e Genérico. Você também pode adicionar modelos de estilo adicionais.  
  
        > [!NOTE]  
        >  Você pode alterar modelos existentes ou adicionar novos modelos editando o arquivo StyleTemplates.xml em \Arquivos de programa\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\Business Intelligence Wizards\Reports\Styles\\<lang\>, em que \<lang> é o idioma que você está usando (por exemplo, se você estiver usando a versão no idioma inglês do [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], o nome da pasta será “EN”). Esta pasta está localizada no computador em que o Designer de Relatórios está instalado. Há duas cópias do arquivo ModelosDeEstilo.xml. Para modificar os estilos aplicados por meio do Assistente de Relatório, edite o arquivo na pasta criada para o idioma que está em uso.  
  
    -   **Nome do relatório.**  A etapa final é nomear o relatório e verificar os campos que serão incluídos no relatório. Quando todas as etapas forem concluídas, o Designer de Relatórios criará o relatório e o adicionará ao projeto de servidor de relatório.  
  
## Para adicionar um novo relatório em branco  
  
1.  No menu **Projeto**, clique em **Adicionar Novo Item**.  
  
2.  Em **Modelos**, clique em **Relatório**.  
  
3.  Clique em **Adicionar**.  
  
     Um novo relatório em branco é adicionado ao projeto e exibido na superfície de design.  
  
## Para adicionar um relatório existente  
  
1.  No menu **Projeto**, clique primeiro em **Adicionar** e depois em **Item Existente**.  
  
2.  Navegue até o local do arquivo .rdl, selecione-o e clique em **Adicionar**.  
  
     O relatório é acrescentado ao projeto na pasta **Relatórios**. Quando você fechar e reabrir o projeto, os relatórios serão classificados pela ordem alfabética.  
  
## Consulte também  
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
  
  