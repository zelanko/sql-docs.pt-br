---
title: 'Lição 3: Criar o relatório pai usando o Assistente de relatório | Microsoft Docs'
ms.custom: ''
ms.date: 03/07/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
ms.assetid: 2f69dcd3-cd6d-45a9-a62a-ba6f5f3179d8
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 331d073082ce68f3ad1b58749256c5a177897e07
ms.sourcegitcommit: 1ab115a906117966c07d89cc2becb1bf690e8c78
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/27/2018
ms.locfileid: "52395061"
---
# <a name="lesson-3-design-the-parent-report-using-the-report-wizard"></a>Lição 3: Criar o relatório pai usando o Assistente de relatório
  Após criar uma conexão de dados e uma tabela de dados para o relatório pai, a próxima etapa será criar o relatório pai usando o Assistente de Relatório no Designer de Relatórios. Para obter mais informações sobre o Designer de Relatórios, consulte [Criar relatórios com o Designer de Relatórios &#40;SSRS&#41;](tools/design-reporting-services-paginated-reports-with-report-designer-ssrs.md).  
  
### <a name="to-design-the-parent-report-using-the-report-wizard"></a>Para criar o relatório pai usando o Assistente de Relatório  
  
1.  Verifique se esse site de nível superior está selecionado no **Gerenciador de Soluções**.  
  
2.  Clique com o botão direito do mouse no site e selecione **Adicionar Novo Item**.  
  
3.  No **Adicionar Novo Item** caixa de diálogo, selecione **Assistente de relatório**, insira um nome para o arquivo de relatório e, em seguida, clique em **adicionar**.  
  
     Isso iniciará o Assistente de Relatório.  
  
4.  No **propriedades do conjunto de dados** página, o **fonte de dados** caixa, selecione o **DataSet1** criado por você na [lição 2: Definir uma Conexão de dados e uma tabela de dados para o relatório pai](lesson-2-define-a-data-connection-and-data-table-for-parent-report.md).  
    A caixa **Conjuntos de dados disponíveis** é atualizada automaticamente com a **DataTable** criada acima.  
  
5.  Clique em **Avançar**.  
  
6.  Na página **Organizar campos** , faça o seguinte:  
  
    1.  Arraste **ProductID**, **Name**, **ProductNumber**, **SafetyStockLevel**e **ReorderLevel** de **Campos disponíveis** até a caixa **Valores** .  
  
    2.  Clique na seta ao lado **SUM (ProductID)**, **SUM (SafetyStockLevel)**, **SUM (reorderlevel)** e desmarque o **soma** seleção.  
  
7.  Clique em **próxima** duas vezes, em seguida, clique em **concluir** para fechar o **Assistente de relatório**.  
  
     Agora você criou o arquivo .rdlc. O arquivo é aberto no Designer de Relatórios. Agora, o tablix que você criou será exibido na superfície de design.  
  
8.  Salve o arquivo .rdlc.  
  
## <a name="next-task"></a>Próxima tarefa  
 Você criou o relatório pai com êxito usando o Assistente de Relatório. Em seguida, você criará uma conexão de dados e uma tabela de dados para o relatório filho.  
  
  
