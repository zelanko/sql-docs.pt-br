---
title: 'Lição 5: Criar o relatório filho usando o Assistente de Relatório | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- reporting-services-native
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 19a3f927-ea97-4f40-a5f8-cd5f2598e4da
caps.latest.revision: 6
author: douglaslM
ms.author: douglasl
manager: mblythe
ms.openlocfilehash: a0c9cea649ecb0f11bdd75d68ce39d48aad8bb92
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36019528"
---
# <a name="lesson-5-design-the-child-report-using-the-report-wizard"></a>Lição 5: Criar o relatório filho usando o Assistente de Relatório
  Após criar uma conexão de dados e uma tabela de dados para o relatório filho, a próxima etapa será criar o relatório filho usando o Assistente de Relatório no Designer de Relatórios. Para obter mais informações sobre o Designer de Relatórios, consulte [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-child-report-using-the-report-wizard"></a>Para criar o relatório filho usando o Assistente de Relatório  
  
1.  Verifique se esse site de nível superior está selecionado no **Gerenciador de Soluções**.  
  
2.  Clique com o botão direito do mouse no site e selecione **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, clique em **Assistente de relatório**, insira um nome para o arquivo de relatório e, em seguida, clique em **adicionar**.  
  
     Isso iniciará o Assistente de Relatório.  
  
4.  No **propriedades de conjunto de dados** página, o **fonte de dados** , clique em **DataSet2**.  
  
     A caixa **Conjuntos de dados disponíveis** é atualizada automaticamente com a DataTable criada.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Organizar campos** , faça o seguinte:  
  
    1.  Arraste **ProductID**, **PurchaseOrderID**, **PurchaseOrderDetailID**, **OrderQty**, **ReceivedQty**, **RejectedQty**e **StockedQty** de **Campos disponíveis** até a caixa **Valores** .  
  
    2.  Clique na seta ao lado de **SUM (ProductID)**, **Sum(PurchaseOrderID)**, **Sum(PurchaseOrderDetailID)**, **Sum(OrderQty)**,  **SUM(ReceivedQty)**, **Sum(RejectedQty)**, e **Sum(StockedQty)** e desmarque o **soma** seleção.  
  
7.  Clique em **próximo** , em seguida, clique duas vezes, **concluir** para fechar o **Assistente de relatório**.  
  
     Agora você criou o arquivo .rdlc. O arquivo é aberto no Designer de Relatórios. Agora, o tablix que você criou será exibido na superfície de design.  
  
8.  Com o arquivo .rdlc aberto, adicione um parâmetro da seguinte maneira:  
  
    1.  Clique em **parâmetros** no **dados de relatório** painel e clique **adicionar parâmetros**.  
  
    2.  Insira **productid** na caixa **Nome** .  
  
    3.  Confirme se a opção **Inteiro** está selecionada na caixa de listagem **Tipo de Dados** .  
  
    4.  Clique em **OK**.  
  
9. Salve o arquivo .rdlc.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou o relatório filho com êxito usando o Assistente de Relatório. Em seguida, você adicionará um controle ReportViewer ao aplicativo de site.  
  
  