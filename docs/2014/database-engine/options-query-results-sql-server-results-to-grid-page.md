---
title: Opções (página resultados da consulta-SQL Server-resultados em grade) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
author: rothja
ms.author: jroth
manager: craigg
ms.openlocfilehash: 9bde39c64fdf2fbabaec85772d4bfa44d86fd1da
ms.sourcegitcommit: 18a7c77be31f9af92ad9d0d3ac5eecebe8eec959
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/26/2020
ms.locfileid: "83856603"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>Opções (página resultados da consulta-SQL Server-resultados em grade)
  Use esta página para especificar as opções de exibição de um conjunto de resultados da consulta em formato de grade. As alterações feitas nessas opções são aplicadas apenas a novas consultas do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para alterar as opções das consultas atuais, clique em **Opções de consulta** no menu **consulta** ou clique com o botão direito do mouse na [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] janela de consulta e selecione **Opções de consulta**. No painel esquerdo da caixa de diálogo **Opções de Consulta**, abaixo de **Resultados**, clique em **Grade**.  
  
## <a name="ui-element-list"></a>Lista de elementos da interface do usuário  
 **Incluir a consulta no conjunto de resultados**  
 Retorna o texto da consulta como parte da saída da consulta.  
  
 **Inclua cabeçalhos de coluna ao copiar ou salvar resultados**  
 Marque essa caixa de seleção para incluir cabeçalhos de coluna quando os resultados forem copiados para a área de transferência ou salvos em um arquivo. Desmarque essa caixa de seleção se desejar que os dados de resultados copiados ou salvos contenham apenas os dados e não os cabeçalhos da coluna.  
  
 **Descartar resultados após a execução**  
 Impede que os resultados de consultas sejam exibidos no painel de revisão. Os resultados são descartados imediatamente após a execução. Especificar essa opção ajuda a economizar memória.  
  
 **Exibir resultados em uma guia separada**  
 Marque essa caixa de seleção para exibir o conjunto de resultados em uma guia, em vez de exibi-lo na parte inferior da janela do documento de consulta.  
  
 **Alternar para a guia Resultados após a execução da consulta**  
 Clique para ajustar automaticamente o foco da tela ao painel de resultados após a execução de uma consulta.  
  
 **Máximo de Caracteres Recuperados**  
 **Dados não XML**:  
  
 Digite um número de 1 a 65535 para especificar o número máximo de caracteres que serão exibidos em cada célula.  
  
> [!NOTE]  
>  Especificar um número grande de caracteres pode fazer com que os dados no conjunto de resultados apareçam truncados. O número máximo de caracteres exibido em cada célula depende do tamanho da fonte. Quando grandes conjuntos de resultados são retornados, um valor alto nessa caixa pode fazer com que o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fique com pouca memória e atrapalhe o desempenho do sistema.  
  
 **Dados XML**:  
  
 Selecione **1 MB**, **2 MB**ou **5 MB**. Selecione **Ilimitado** para recuperar todos os caracteres.  
  
 **Restaurar Padrões**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
