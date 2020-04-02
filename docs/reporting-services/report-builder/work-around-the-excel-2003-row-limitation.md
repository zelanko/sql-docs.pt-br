---
title: Solução do problema de limitação de linhas do Excel 2003 | Microsoft Docs
description: Você pode contornar a limitação de linhas do Excel 2003 ao exportar relatórios paginados para o Excel forçando uma quebra de página após um determinado número de linhas.
ms.date: 03/16/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-native
ms.technology: report-builder
ms.topic: conceptual
ms.assetid: a4c8700b-bef5-4440-a99c-bba5dcc46bfd
author: maggiesMSFT
ms.author: maggies
ms.openlocfilehash: 940f5fd22d35ac0a90106c7a325e435e1d479bc4
ms.sourcegitcommit: ff82f3260ff79ed860a7a58f54ff7f0594851e6b
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/29/2020
ms.locfileid: "80290723"
---
# <a name="work-around-the-excel-2003-row-limitation"></a>Work Around the Excel 2003 Row Limitation
  Este tópico explica como resolver a limitação de linhas do Excel 2003 quando você exporta relatórios paginados para o Excel. A solução alternativa é para um relatório que contém apenas uma tabela.  
  
> [!IMPORTANT]  
>  A extensão de renderização do [!INCLUDE[ofprexcel](../../includes/ofprexcel-md.md)] 2003 (.xls) foi preterida. Para obter mais informações, consulte [Recursos preteridos no SQL Server Reporting Services no SQL Server 2016](../../reporting-services/deprecated-features-in-sql-server-reporting-services-ssrs.md).  
  
 O Excel 2003 oferece suporte a um máximo de 65.536 linhas por planilha. Você pode solucionar essa limitação forçando uma quebra de página explícita depois de um determinado número de linhas. O renderizador do Excel cria uma nova planilha para cada quebra de página explícita.  
  
### <a name="to-create-an-explicit-page-break"></a>Para criar uma quebra de página explícita  
  
1.  Abra o relatório no [!INCLUDE[ss_dtbi](../../includes/ss-dtbi-md.md)] ou no portal da Web do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] .  
  
2.  Clique com o botão direito do mouse na linha Dados da tabela e clique em **Adicionar Grupo** > **Grupo Pai** para adicionar um grupo de tabelas externo.  
  
     ![Selecionar o grupo pai](../../reporting-services/report-builder/media/datarow-selectparentgroup.png "Selecionar o grupo pai")  
  
3.  Digite a fórmula a seguir na caixa de expressão **Agrupar por** e clique em **OK** para adicionar o grupo pai.  
  
     =Int((RowNumber(Nothing)-1)/65000)  
  
     A fórmula atribui um número a cada conjunto de 65000 linhas no conjunto de dados. Quando uma quebra de página é definida para o grupo, a expressão resulta em uma quebra de página a cada 65000 linhas.  
  
     A adição do grupo de tabelas externo adiciona uma coluna de grupo ao relatório.  
  
4.  Exclua a coluna de grupo clicando com o botão direito do mouse no cabeçalho de coluna, clicando em **Excluir Colunas**, selecionando **Excluir colunas apenas**e clicando em **OK**.  
  
     ![Excluir uma coluna do grupo](../../reporting-services/report-builder/media/groupcolumn-delete-updated.png "Excluir uma coluna do grupo")  
  
5.  Clique com o botão direito do mouse em **Grupo 1** na seção **Grupos de Linhas** e clique em **Propriedades do Grupo**.  
  
     ![Exibir propriedades do grupo](../../reporting-services/report-builder/media/groupproperties-updated.png "Exibir propriedades do grupo")  
  
6.  Na página **Classificação** da caixa de diálogo **Propriedades do Grupo** , selecione a opção de classificação padrão e clique em **Excluir**.  
  
     ![Excluir classificação padrão](../../reporting-services/report-builder/media/groupproperties-sorting-updated.png "Excluir classificação padrão")  
  
7.  Na página **Quebras de Página** , clique em **Entre cada instância de um grupo** e clique em **OK**.  
  
     ![Definir quebras de página](../../reporting-services/report-builder/media/groupproperties-pagebreaks-updated.png "Definir quebras de página")  
  
8.  Salve o relatório. Quando você exportá-lo para o Excel, a exportação será realizada para várias planilhas, e cada planilha conterá um máximo de 65000 linhas.  
  
  
