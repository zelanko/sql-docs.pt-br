---
title: Criando um relatório de tabela básico (Tutorial do SSRS) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
helpviewer_keywords:
- walkthroughs [Reporting Services]
- tutorials [Reporting Services]
- reports [Reporting Services], creating
ms.assetid: 3b539b4b-26f2-4c0b-b506-80f175679a46
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: 08ed0c207b92075952ffc71669b45100e4ff7d06
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66109677"
---
# <a name="create-a-basic-table-report-ssrs-tutorial"></a>Criando um relatório de tabela básico (Tutorial do SSRS)
  Este tutorial foi criado para ajudar a criar uma tabela básica com base no banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] usando o Designer de Relatórios. Você também pode usar o Construtor de Relatórios ou o Assistente de Relatório para criar relatórios. Neste tutorial, você irá criar um projeto de relatório, configurar informações de conexão, definir uma consulta, adicionar uma região de dados de Tabela, agrupar e totalizar alguns campos e visualizar o relatório.  
  
> [!NOTE]  
>  Para concluir este tutorial, você deve estar executando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em modo nativo. Se você estiver executando o [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] em modo integrado do SharePoint, as etapas que usam URLs de servidor de relatório não funcionarão. Para obter mais informações [!INCLUDE[ssRSnoversion](../includes/ssrsnoversion-md.md)] sobre modos, consulte [Reporting Services servidor de relatório](reporting-services-report-server.md).  
  
## <a name="requirements"></a>Requisitos  
 Para que você possa usar o tutorial, os itens a seguir devem estar instalados no sistema:  
  
-   [!INCLUDE[msCoName](../includes/msconame-md.md)][!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] mecanismo de banco de dados.  
  
-   O banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  Para obter mais informações, consulte [Adventure Works para SQL Server 2012 (Adventure Works para SQL Server 2012)](https://go.microsoft.com/fwlink/?LinkId=245471) (https://go.microsoft.com/fwlink/?LinkId=245471).. Para obter mais informações sobre o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] suporte para bancos de dados de exemplo e [!INCLUDE[ssExpress](../includes/ssexpress-md.md)]código de exemplo para o, consulte [visão geral de bancos de dados e exemplos](https://go.microsoft.com/fwlink/?LinkId=110391) no site do CodePlex.  
  
-   [!INCLUDE[ssRSCurrent](../includes/ssrscurrent-md.md)].  
  
-   [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)].  
  
    > [!NOTE]  
    >  [!INCLUDE[ssNote64Samp](../includes/ssnote64samp-md.md)]  
  
 Também é necessário ter permissões somente leitura para recuperar dados do banco de dados [!INCLUDE[ssSampleDBobject](../includes/sssampledbobject-md.md)] .  
  
## <a name="tasks"></a>Tarefas  
 [Lição 1: Criando um projeto do Servidor de Relatório &#40;Reporting Services&#41;](lesson-1-creating-a-report-server-project-reporting-services.md)  
  
 [Lição 2: Especificando informações sobre conexão &#40;Reporting Services&#41;](lesson-2-specifying-connection-information-reporting-services.md)  
  
 [Lição 3: Definindo um conjunto de dados para o relatório de tabela &#40;Reporting Services&#41;](lesson-3-defining-a-dataset-for-the-table-report-reporting-services.md)  
  
 [Lição 4: Adicionando uma tabela ao relatório &#40;Reporting Services&#41;](lesson-4-adding-a-table-to-the-report-reporting-services.md)  
  
 [Lição 5: Formatando um relatório &#40;Reporting Services&#41;](lesson-5-formatting-a-report-reporting-services.md)  
  
 [Lição 6: Adicionando agrupamentos e totais &#40;Reporting Services&#41;](lesson-6-adding-grouping-and-totals-reporting-services.md)  
  
> [!NOTE]  
>  Ao revisar os tutoriais, recomendamos que você adicione os botões **Avançar** e **anterior** à barra de ferramentas do Visualizador de documentos. Para obter mais informações, confira:  
  
## <a name="see-also"></a>Consulte Também  
 [Tutoriais do Reporting Services &#40;SSRS&#41;](reporting-services-tutorials-ssrs.md)  
  
  
