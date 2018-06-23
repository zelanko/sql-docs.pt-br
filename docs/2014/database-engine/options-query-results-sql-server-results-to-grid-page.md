---
title: Opções (resultados SQL Server-resultados da consulta para a página grade) | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.QueryResults.SqlServer.SQLResultsToGrid
ms.assetid: f88a0f5c-e800-473b-ae23-c3943de5ed63
caps.latest.revision: 25
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: eafa41250705c453776947a3da56c86f9e3c0f90
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36117029"
---
# <a name="options-query-results-sql-server-results-to-grid-page"></a>Opções (resultados SQL Server-resultados da consulta para a página grade)
  Use esta página para especificar as opções de exibição de um conjunto de resultados da consulta em formato de grade. As alterações feitas nessas opções são aplicadas apenas a novas consultas do [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)]. Para alterar as opções das consultas atuais, clique em **Opções de Consulta** no menu **Consulta** ou clique com o botão direito do mouse na janela Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecione **Opções de Consulta**. No painel esquerdo da caixa de diálogo **Opções de Consulta**, abaixo de **Resultados**, clique em **Grade**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **Incluir a consulta no conjunto de resultados**  
 Retorna o texto da consulta como parte da saída da consulta.  
  
 **Incluir cabeçalhos de coluna ao copiar ou salvar os resultados**  
 Marque essa caixa de seleção para incluir cabeçalhos de coluna quando os resultados forem copiados para a área de transferência ou salvos em um arquivo. Desmarque essa caixa de seleção se desejar que os dados de resultados copiados ou salvos contenham apenas os dados e não os cabeçalhos da coluna.  
  
 **Descartar resultados após a execução**  
 Impede que os resultados de consultas sejam exibidos no painel de revisão. Os resultados são descartados imediatamente após a execução. Especificar essa opção ajuda a economizar memória.  
  
 **Exibir resultados em uma guia separada**  
 Marque essa caixa de seleção para exibir o conjunto de resultados em uma guia, em vez de exibi-lo na parte inferior da janela do documento de consulta.  
  
 **Alternar para a guia resultados após a execução da consulta**  
 Clique para ajustar automaticamente o foco da tela ao painel de resultados após a execução de uma consulta.  
  
 **Máximo de caracteres recuperados**  
 **Dados não XML**:  
  
 Digite um número de 1 a 65535 para especificar o número máximo de caracteres que serão exibidos em cada célula.  
  
> [!NOTE]  
>  Especificar um número grande de caracteres pode fazer com que os dados no conjunto de resultados apareçam truncados. O número máximo de caracteres exibido em cada célula depende do tamanho da fonte. Quando grandes conjuntos de resultados são retornados, um valor alto nessa caixa pode fazer com que o [!INCLUDE[ssManStudioFull](../includes/ssmanstudiofull-md.md)] fique com pouca memória e atrapalhe o desempenho do sistema.  
  
 **Dados XML**:  
  
 Selecione **1 MB**, **2 MB**ou **5 MB**. Selecione **Ilimitado** para recuperar todos os caracteres.  
  
 **Redefinir para padrão**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  