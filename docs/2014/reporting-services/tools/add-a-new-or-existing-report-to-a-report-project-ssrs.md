---
title: Adicionar um relatório novo ou existente a um projeto de relatório (SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: b150c7e42cf5389783706138c055c4a7fdea9b05
ms.sourcegitcommit: 8d6fb6bbe3491925909b83103c409effa006df88
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/22/2019
ms.locfileid: "59960592"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Adicionar um relatório novo ou existente a um projeto de relatório (SSRS)
  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode adicionar um relatório novo usando o Assistente de Relatório ou acrescentando um novo relatório em branco ao projeto. Também é possível adicionar um relatório existente. Depois de adicionar um relatório, você poderá ver o nome do relatório listado na pasta **Relatórios** do seu projeto.  
  
> [!NOTE]  
>  Para visualizar um relatório com fontes de dados existentes, é preciso ter as permissões para a fonte de dados do cliente que está criando o relatório. Para obter mais informações, consulte [criar uma fonte de dados compartilhada ou um inserido &#40;SSRS&#41;](../create-an-embedded-or-shared-data-source-ssrs.md).  
  
 Depois de adicionar um relatório, é possível definir as fontes de dados e os conjuntos de dados, e criar um layout de relatório. Para começar, consulte [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../create-a-basic-table-report-ssrs-tutorial.md) ou [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../report-design/tables-report-builder-and-ssrs.md).  
  
### <a name="to-add-a-new-report-using-the-report-wizard"></a>Para adicionar um novo relatório usando o Assistente de Relatórios  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Relatórios e clique em **Adicionar Novo Relatório**. A caixa de diálogo **Assistente de Relatório** é aberta.  
  
     O assistente conduzirá você pela criação de uma fonte de dados, a criação de um conjunto de dados com uma consulta, a definição de grupos, a escolha de um estilo que inclua cor e fonte, e a criação do relatório. As etapas incluem:  
  
    -   **Selecionar uma fonte de dados.** A primeira etapa ao criar um relatório é definir uma fonte de dados. O Assistente de Relatório apresenta uma lista de todas as fontes de dados compartilhadas no projeto de relatório, além de uma opção para criar uma nova fonte de dados.  
  
    -   **Criar uma consulta.** A próxima etapa é criar uma consulta. É possível digitar a cadeia de caracteres da consulta, gerar no Designer de Consulta ou importar uma consulta a partir de outro relatório. Para obter informações sobre Designers de Consulta, consulte [Designers de Consulta do Reporting Services](../reporting-services-query-designers.md).  
  
    -   **Escolher um tipo de relatório.** A próxima etapa é selecionar o tipo de relatório desejado. Você pode optar por um relatório tabular ou de matriz. Um relatório tabular tem um número fixo de colunas. Uma relatório de matriz ou de tabulação cruzada apresenta um número variável de colunas com base nos resultados da consulta. Um relatório de mapa exibe dados analíticos em relação a um plano de fundo geográfico.  
  
    -   **Escolha um estilo.** A próxima etapa é aplicar um estilo ao relatório que usa um modelo de estilo. Selecione um modelo para aplicar estilos como fonte, cor e estilo de borda ao relatório. Designer de relatórios fornece seis modelos de estilo: Ardósia, floresta, corporativa, negrito, azul-marinho e genérico. Você também pode adicionar modelos de estilo adicionais.  
  
        > [!NOTE]  
        >  Você pode alterar modelos existentes ou adicionar novos, editando o arquivo Styletemplates XML no \Program Files\Microsoft Visual Studio 10.0\Common7\IDE\PrivateAssemblies\Business Intelligence Wizards\Reports\Styles\\< lang\>pasta, onde \<lang > é o idioma que você está usando (por exemplo, se você estiver usando a versão do idioma inglês [!INCLUDE[vsprvs](../../includes/vsprvs-md.md)], o nome da pasta será "EN"). Esta pasta está localizada no computador em que o Designer de Relatórios está instalado. Há duas cópias do arquivo ModelosDeEstilo.xml. Para modificar os estilos aplicados por meio do Assistente de Relatório, edite o arquivo na pasta criada para o idioma que está em uso.  
  
    -   **Nome do relatório.**  A etapa final é nomear o relatório e verificar os campos que serão incluídos no relatório. Quando todas as etapas forem concluídas, o Designer de Relatórios criará o relatório e o adicionará ao projeto de servidor de relatório.  
  
### <a name="to-add-a-new-blank-report"></a>Para adicionar um novo relatório em branco  
  
1.  No menu **Projeto** , clique em **Adicionar Novo Item**.  
  
2.  Em **Modelos**, clique em **Relatório**.  
  
3.  Clique em **Adicionar**.  
  
     Um novo relatório em branco é adicionado ao projeto e exibido na superfície de design.  
  
### <a name="to-add-an-existing-report"></a>Para adicionar um relatório existente  
  
1.  Dos **Project** menu, clique em **Add**e, em seguida, **Item existente**.  
  
2.  Navegue até o local do arquivo .rdl, selecione-o e clique em **Adicionar**.  
  
     O relatório é acrescentado ao projeto na pasta **Relatórios** . Quando você fechar e reabrir o projeto, os relatórios serão classificados pela ordem alfabética.  
  
## <a name="see-also"></a>Consulte também  
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../reporting-services-tutorials-ssrs.md)  
  
  
