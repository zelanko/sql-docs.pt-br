---
title: Adicionar um relatório novo ou existente a um projeto de relatório | Microsoft Docs
ms.date: 03/17/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: tools
ms.topic: conceptual
helpviewer_keywords:
- reports [Reporting Services], creating
ms.assetid: 8bc0bb53-ad8a-464d-bb6a-7fea5fa62c5c
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: d9afb31b4c2793e7196fda36280fed3d590a32cf
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "77077895"
---
# <a name="add-a-new-or-existing-report-to-a-report-project-ssrs"></a>Adicionar um relatório novo ou existente a um projeto de relatório (SSRS)
  Em [!INCLUDE[ssBIDevStudioFull](../../includes/ssbidevstudiofull-md.md)], você pode adicionar um novo relatório paginado do [!INCLUDE[ssRSnoversion_md](../../includes/ssrsnoversion-md.md)] usando o Assistente de Relatório ou acrescentando um novo relatório em branco ao projeto. Também é possível adicionar um relatório existente. Depois de adicionar um relatório, você poderá ver o nome do relatório listado na pasta **Relatórios** do seu projeto.  
  
> [!NOTE]  
>  Para visualizar um relatório com fontes de dados existentes, é preciso ter as permissões para a fonte de dados do cliente que está criando o relatório. Para obter mais informações, consulte [Conexões de dados, fontes de dados e cadeias de conexão](../../reporting-services/report-data/data-connections-data-sources-and-connection-strings-report-builder-and-ssrs.md).  
  
 Depois de adicionar um relatório, é possível definir as fontes de dados e os conjuntos de dados, e criar um layout de relatório. Para começar, consulte [Criar um relatório de tabela básico &#40;Tutorial do SSRS&#41;](../../reporting-services/create-a-basic-table-report-ssrs-tutorial.md) ou [Tabelas &#40;Construtor de Relatórios e SSRS&#41;](../../reporting-services/report-design/tables-report-builder-and-ssrs.md).  
  
## <a name="to-add-a-new-report-using-the-report-wizard"></a>Para adicionar um novo relatório usando o Assistente de Relatórios  
  
1.  No Gerenciador de Soluções, clique com o botão direito do mouse na pasta Relatórios e clique em **Adicionar Novo Relatório**. A caixa de diálogo **Assistente de Relatório** é aberta.  
  
     O assistente orientará você pela criação de uma fonte de dados, criação de um conjunto de dados com uma consulta, definição de grupos, especificação de um layout e criação do relatório. As etapas são as seguintes:  
  
    -   **Selecionar uma fonte de dados.** A primeira etapa ao criar um relatório é definir uma fonte de dados. O Assistente de Relatório apresenta uma lista de todas as fontes de dados compartilhadas no projeto de relatório, além de uma opção para criar uma nova fonte de dados.  
  
    -   **Criar uma consulta.** A próxima etapa é criar uma consulta. É possível digitar a cadeia de caracteres da consulta, gerar no Designer de Consulta ou importar uma consulta a partir de outro relatório. Para obter informações sobre Designers de Consulta, consulte [Designers de Consulta do Reporting Services](https://msdn.microsoft.com/library/07efd3f1-804f-45f7-b62a-3e727a3d9835).  
  
    -   **Escolher um tipo de relatório.** A próxima etapa é selecionar o tipo de relatório desejado. Você pode optar por um relatório tabular ou de matriz. Um relatório tabular tem um número fixo de colunas. Uma relatório de matriz ou de tabulação cruzada apresenta um número variável de colunas com base nos resultados da consulta. Um relatório de mapa exibe dados analíticos em relação a um plano de fundo geográfico.  
  
    -   **Nome do relatório.**  A etapa final é nomear o relatório e verificar os campos que serão incluídos no relatório. Quando todas as etapas forem concluídas, o Designer de Relatórios criará o relatório e o adicionará ao projeto de servidor de relatório.  
  
## <a name="to-add-a-new-blank-report"></a>Para adicionar um novo relatório em branco  
  
1.  No menu **Projeto** , clique em **Adicionar Novo Item**.  
  
2.  Em **Modelos**, clique em **Relatório**.  
  
3.  Clique em **Adicionar**.  
  
     Um novo relatório em branco é adicionado ao projeto e exibido na superfície de design.  
  
## <a name="to-add-an-existing-report"></a>Para adicionar um relatório existente  
  
1.  No menu **Projeto** , clique primeiro em **Adicionar**e depois em  **Item Existente**.  
  
2.  Navegue até o local do arquivo .rdl, selecione-o e clique em **Adicionar**.  
  
     O relatório é acrescentado ao projeto na pasta **Relatórios** . Quando você fechar e reabrir o projeto, os relatórios serão classificados pela ordem alfabética.  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais do Reporting Services &#40;SSRS&#41;](../../reporting-services/reporting-services-tutorials-ssrs.md)  
 Mais perguntas? [Experimente o fórum do Reporting Services](https://go.microsoft.com/fwlink/?LinkId=620231)
  
  
