---
title: 'Tarefa 10: adicionando a transformação de grupo difuso para identificar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: data-quality-services
ms.topic: conceptual
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
author: lrtoyou1223
ms.author: lle
manager: craigg
ms.openlocfilehash: 48e233c6f2c7a55bf2420825b9fb3064db6e89e1
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "65481248"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>Tarefa 10: Adicionando a Transformação Grupo Difuso para identificar duplicatas
  Nesta tarefa, você adiciona uma Transformação Grupo Difuso ao fluxo de dados. A transformação Grupo Difuso pode ajudar a identificar duplicatas nos dados de origem. Consulte [transformação Agrupamento Difuso](../integration-services/data-flow/transformations/fuzzy-grouping-transformation.md) para obter mais detalhes.  
  
1.  Arraste e solte a transformação de **grupo difuso** em **outras transformações** na **caixa de ferramentas do SSIS** para a guia **fluxo de dados** em **combinar registros corretos e corrigidos**.  
  
2.  Clique com o botão direito do mouse em transformação de **grupo difuso** na guia **fluxo de dados** e clique em **renomear**. Digite **Agrupar fornecedores com IDs correspondentes** e pressione **Enter**.  
  
3.  Conectar **Combine registros corretos e corrigidos** para **Agrupar fornecedores com IDs correspondentes** usando o conector azul.  
  
     ![Conexão ao grupo Fornecedores com IDs correspondentes](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Conexão ao grupo Fornecedores com IDs correspondentes")  
  
4.  Clique duas vezes em **Agrupar fornecedores com IDs correspondentes**.  
  
5.  No **Editor de transformação grupo difuso**, clique em **novo** ao lado de **OLE DB lista suspensa Gerenciador de conexões** para iniciar a caixa de diálogo **Configurar OLE DB Gerenciador de conexões** .  
  
6.  Na caixa de diálogo, clique em **novo** para iniciar a caixa de diálogo **Gerenciador de conexões** .  
  
7.  Digite **(local)** ou **ponto** (.) para o nome do servidor.  
  
8.  Selecione **MDS** para **selecionar ou insira um campo nome do banco de dados** . Você usará o banco de dados do MDS como o armazenamento temporário para a **transformação do grupo difuso**. A transformação **Agrupamento Difuso** requer uma conexão com uma instância do SQL Server para criar as tabelas de SQL Server temporárias que o algoritmo de transformação requer para realizar seu trabalho. Você pode criar um banco de dados ou usar outro banco de dados existente para essa finalidade.  
  
9. Clique em **testar conexão** para testar a conexão e clique em **OK** na caixa de mensagem.  
  
10. Na caixa de diálogo **Gerenciador de conexões** , clique em **OK**.  
  
11. Selecione **(local). MDS** (ou **localhost. MDS**) na **lista de conexões de dados** e clique em **OK**.  
  
12. No **Editor de transformação Agrupamento Difuso**, confirme se **(local). MDS** ou **localhost. O MDS** é selecionado para o **Gerenciador de conexões OLE DB**.  
  
13. Alterne para a guia **colunas** .  
  
14. Selecione (caixa de seleção) **SupplierID_Output** na lista de **colunas de entrada disponíveis**. Para configurar a transformação, selecione as colunas de entrada a serem usadas ao identificar duplicatas. Para manter a simplicidade, use apenas SupplierID nesta etapa.  
  
     ![Editor de Transformação Agrupamento Difuso](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "Editor de Transformação Agrupamento Difuso")  
  
15. Clique em **OK** para fechar o **Editor de transformação grupo difuso**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 11: Adicionando a Transformação Divisão Condicional para filtrar duplicatas](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  
