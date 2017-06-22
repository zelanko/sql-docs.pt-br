---
title: "Lição 5: Criar o relatório filho usando o Assistente de relatório | Microsoft Docs"
ms.custom: 
ms.date: 05/18/2016
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
applies_to:
- SQL Server 2016
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 8
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: Machine Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 285ade0eaf63fee0733fcfcb9e8f627e8c666a6b
ms.contentlocale: pt-br
ms.lasthandoff: 06/22/2017

---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lição 5: Criar o relatório filho usando o Assistente de Relatório
Após criar uma conexão de dados e uma tabela de dados para o relatório filho, a próxima etapa será criar o relatório filho usando o Assistente de Relatório no Designer de Relatórios. Para obter mais informações sobre o Designer de Relatórios, consulte [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](../reporting-services/tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Para criar o relatório filho usando o Assistente de Relatório  
  
1.  Verifique se esse site de nível superior está selecionado no **Gerenciador de Soluções**.  
  
2.  Clique com o botão direito do mouse no site e selecione **Adicionar Novo Item**.  
  
3.  Na caixa de diálogo **Adicionar Novo Item** , clique em **Assistente de Relatório**, insira um nome para o arquivo de relatório e selecione **Adicionar**.  
  
    Isso iniciará o Assistente de Relatório.  
  
4.  Na página **Propriedades do Conjunto de Dados** , na caixa **Fonte de dados** , selecione **DataSet2**.  
  
    A caixa **Conjuntos de dados disponíveis** é atualizada automaticamente com a DataTable criada.  
  
5.  Selecione **Avançar**.  
  
6.  Na página **Organizar campos** , faça o seguinte:  
  
    1.  Arraste **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**e **StockedQty** de **Campos disponíveis** até a caixa **Valores** .  
  
    2.  Clique na seta ao lado de **Sum(ProductID)**, **Sum(PurchaseOrderID)**, **Sum(PurchaseOrderDetailID)**, **Sum(OrderQty)**, **Sum(ReceivedQty)**, **Sum(RejectedQty)**e **Sum(StockedQty)** e desmarque a seleção **Sum** .  
  
7.  Selecione **Avançar** duas vezes e **Concluir** para fechar o **Assistente de Relatório**.  
  
    Agora você criou o arquivo .rdlc. O arquivo é aberto no Designer de Relatórios. Agora, o tablix que você criou será exibido na superfície de design.  
  
8.  Com o arquivo .rdlc aberto, adicione um parâmetro da seguinte maneira:  
  
    1.  Clique com o botão direito do mouse em **Parâmetros** no painel **Dados do Relatório** e selecione **Adicionar Parâmetros**.  
  
    2.  Insira **productid** na caixa **Nome** .  
  
    3.  Confirme se a opção **Inteiro** está selecionada na caixa de listagem **Tipo de Dados** .  
  
    4.  Clique em **OK**.  
  
9. Salve o arquivo .rdlc.  
  
## <a name="next-task"></a>Próxima tarefa  
Você criou o relatório filho com êxito usando o Assistente de Relatório. Em seguida, você adicionará um controle ReportViewer ao aplicativo de site. Consulte [Lição 6: Adicionar um controle ReportViewer ao aplicativo](../reporting-services/lesson-6-add-a-reportviewer-control-to-the-application.md).  
  
  
  


