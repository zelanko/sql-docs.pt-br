---
title: "Solução alternativa a limitação de linhas do Excel 2003 | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
caps.latest.revision: 12
author: maggiesMSFT
ms.author: maggies
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: 0eb007a5207ceb0b023952d5d9ef6d95986092ac
ms.openlocfilehash: 8533cd39c8a3d5efde78fee3e045eb744d562a97
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  Este tópico explica como resolver a limitação de linhas do Excel 2003 quando você exporta relatórios paginados para o Excel. A solução alternativa é para um relatório que contém apenas uma tabela.  
  
> [!IMPORTANT]  
>  A extensão de renderização do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 (.xls) foi preterida. Para obter mais informações, consulte [Recursos preteridos no SQL Server Reporting Services no SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 O Excel 2003 oferece suporte a um máximo de 65.536 linhas por planilha. Você pode solucionar essa limitação forçando uma quebra de página explícita depois de um determinado número de linhas. O renderizador do Excel cria uma nova planilha para cada quebra de página explícita.  
  
### <a name="to-create-an-explicit-page-break"></a>Para criar uma quebra de página explícita  
  
1.  Abra o relatório no [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] ou no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Clique com o botão direito do mouse na linha Dados da tabela e clique em **Adicionar Grupo** > **Grupo Pai** para adicionar um grupo de tabelas externo.  
  
     ![Selecione o grupo pai](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "selecione o grupo pai")  
  
3.  Digite a fórmula a seguir na caixa de expressão **Agrupar por** e clique em **OK** para adicionar o grupo pai.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     A fórmula atribui um número a cada conjunto de 65000 linhas no conjunto de dados. Quando uma quebra de página é definida para o grupo, a expressão resulta em uma quebra de página a cada 65000 linhas.  
  
     A adição do grupo de tabelas externo adiciona uma coluna de grupo ao relatório.  
  
4.  Exclua a coluna de grupo clicando com o botão direito do mouse no cabeçalho de coluna, clicando em **Excluir Colunas**, selecionando **Excluir colunas apenas**e clicando em **OK**.  
  
     ![Excluir uma coluna de grupo](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "excluir uma coluna de grupo")  
  
5.  Clique com o botão direito do mouse em **Grupo 1** na seção **Grupos de Linhas** e clique em **Propriedades do Grupo**.  
  
     ![Exibir propriedades do grupo](../../reporting-services/report-builder/media/groupproperties-updated.png "exibir propriedades do grupo")  
  
6.  Na página **Classificação** da caixa de diálogo **Propriedades do Grupo** , selecione a opção de classificação padrão e clique em **Excluir**.  
  
     ![Excluir classificação padrão](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "excluir classificação padrão")  
  
7.  Na página **Quebras de Página** , clique em **Entre cada instância de um grupo** e clique em **OK**.  
  
     ![Definir quebras de página](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "definir quebras de página")  
  
8.  Salve o relatório. Quando você exportá-lo para o Excel, a exportação será realizada para várias planilhas, e cada planilha conterá um máximo de 65000 linhas.  
  
  
