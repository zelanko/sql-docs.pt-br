---
title: 'Tarefa 10: Adicionando a transformação grupo difuso para identificar duplicatas | Microsoft Docs'
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- data-quality-services
- integration-services
- master-data-services
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 90b2b323-babd-464a-8914-9dc5e66aca74
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: cf9ad3dff4737d7308e7ec3434985b18015f29d8
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36013481"
---
# <a name="task-10-adding-fuzzy-group-transform-to-identify-duplicates"></a>Tarefa 10: Adicionando a Transformação Grupo Difuso para identificar duplicatas
  Nesta tarefa, você adiciona uma Transformação Grupo Difuso ao fluxo de dados. A transformação Grupo Difuso pode ajudar a identificar duplicatas nos dados de origem. Consulte [transformação agrupamento difuso](http://msdn.microsoft.com/library/ms141764.aspx) para obter mais detalhes.  
  
1.  Arraste e solte **grupo difuso** transformar no **outras transformações** no **caixa de ferramentas do SSIS** para o **de fluxo de dados** guia  **Combinar registros corretos e corrigidos**.  
  
2.  Clique com botão direito **grupo difuso** transformar no **de fluxo de dados** guia e, em seguida, clique em **Renomear**. Tipo **agrupar fornecedores com IDs correspondentes** e pressione **ENTER**.  
  
3.  Conecte-se **combinar registros corretos e corrigidos** para **agrupar fornecedores com IDs correspondentes** usando o conector azul.  
  
     ![Conexão ao grupo fornecedores com IDs correspondentes](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-01.jpg "Conexão ao grupo fornecedores com IDs correspondentes")  
  
4.  Clique duas vezes em **agrupar fornecedores com IDs correspondentes**.  
  
5.  No **Editor de transformação grupo difuso**, clique em **novo** lado **lista suspensa de Gerenciador de Conexão OLE DB** iniciar **configurar OLE DB Conexão Gerenciador de** caixa de diálogo.  
  
6.  Na caixa de diálogo, clique em **novo** iniciar **Gerenciador de Conexão** caixa de diálogo.  
  
7.  Tipo **(local)** ou **período** (.) para o nome do servidor.  
  
8.  Selecione **MDS** para **selecionar ou digitar um nome de banco de dados** campo. Você usará o banco de dados do MDS como o armazenamento temporário para o **transformação grupo difuso**. O **agrupamento difuso** transformação requer uma conexão a uma instância do SQL Server para criar as tabelas temporárias do SQL Server que o algoritmo de transformação necessita para fazer seu trabalho. Você pode criar um banco de dados ou usar outro banco de dados existente para essa finalidade.  
  
9. Clique em **Testar Conexão** para testar a conexão e clique em **Okey** na caixa de mensagem.  
  
10. No **Gerenciador de Conexão** caixa de diálogo, clique em **Okey**.  
  
11. Selecione **(local). MDS** (ou **localhost. MDS**) da **lista de conexões de dados** e clique em **Okey**.  
  
12. No **Editor de transformação agrupamento difuso**, confirme se **(local). MDS** ou **localhost. MDS** é selecionado para o **Gerenciador de Conexão OLE DB**.  
  
13. Alterne para o **colunas** guia.  
  
14. Selecione (caixa de seleção) **SupplierID_Output** da lista de **colunas de entrada disponíveis**. Para configurar a transformação, selecione as colunas de entrada a serem usadas ao identificar duplicatas. Para manter a simplicidade, use apenas SupplierID nesta etapa.  
  
     ![Editor de transformação agrupamento difuso](../../2014/tutorials/media/et-addingfgttoidentifyduplicates-02.jpg "Editor de transformação agrupamento difuso")  
  
15. Clique em **Okey** para fechar o **Editor de transformação grupo difuso**.  
  
## <a name="next-step"></a>Próxima etapa  
 [Tarefa 11: Adicionando a Transformação Divisão Condicional para filtrar duplicatas](../../2014/tutorials/task-11-adding-conditional-split-transform-to-filter-duplicates.md)  
  
  