---
title: Adicionar um log para contadores de desempenho de fluxo de dados | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- performance counters [Integration Services]
- counters [Integration Services]
- logs [Integration Services], data flow counters
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 76c85de1e9e8c294ab9db1f887f2b417b321d663
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66062056"
---
# <a name="add-a-log-for-data-flow-performance-counters"></a>Adicionar um log para contadores de desempenho de fluxo de dados
  Este procedimento descreve como adicionar um log para os contadores de desempenho fornecidos pelo mecanismo de fluxo de dados.  
  
> [!NOTE]  
>  se você instalar o [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] em um computador que está executando o [!INCLUDE[winxpsvr](../includes/winxpsvr-md.md)]e atualizar o computador para o [!INCLUDE[firstref_longhorn](../includes/firstref-longhorn-md.md)], o processo de atualização removerá os contadores de desempenho do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] do computador. Para restaurar os contadores de desempenho do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] no computador, execute a Instalação do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] em modo de reparo.  
  
### <a name="to-add-logging-of-performance-counters"></a>Para adicionar registros de contadores de desempenho  
  
1.  No **Painel de Controle**, se você estiver usando a exibição Clássica, clique em **Ferramentas Administrativas**. Se você estiver usando a exibição Categoria, clique em **Desempenho e Manutenção** e clique em **Ferramentas Administrativas**.  
  
2.  Clique em **Desempenho**.  
  
3.  Na caixa de diálogo **Desempenho** , expanda **Logs e Alertas de Desempenho**, clique com o botão direito do mouse em **Logs do Contador**e clique em **Novas Configurações de Log**. Digite o nome do log. Por exemplo, digite **MyLog**.  
  
4.  Clique em **OK**.  
  
5.  Na caixa de diálogo **MyLog** , clique em **Adicionar Contadores**.  
  
6.  Clique em **Usar contadores locais do computador** para registrar contadores de desempenho no computador local ou clique em **Selecionar contadores do computador** e selecione um computador da lista para registrar os contadores de desempenho no computador especificado.  
  
7.  Na caixa de diálogo **Adicionar contadores** , selecione **SQL Server:SSIS Pipeline** na lista **Objeto de desempenho** .  
  
8.  Para selecionar contadores de desempenho, execute um dos seguintes procedimentos:  
  
    -   Selecione **Todos os contadores** para registrar todos os contadores de desempenho.  
  
    -   Selecione **Selecionar contadores na lista** e selecione o contador de desempenho a ser usado.  
  
9. Clique em **Adicionar**.  
  
10. Clique em **fechar**  
  
11. Na caixa de diálogo **MyLog** , examine a lista de registro de contadores de desempenho na lista **Contadores** .  
  
12. Para adicionar contadores extras, repitas as etapas de 5 a 10.  
  
13. Clique em **OK**.  
  
    > [!NOTE]  
    >  Você deve iniciar o serviço Logs e Alertas de Desempenho usando uma conta local ou uma conta de domínio que seja um membro do grupo Administradores.  
  
## <a name="see-also"></a>Consulte Também  
 [Contadores de desempenho](performance/performance-counters.md)   
 [Exibir entradas de log na janela Eventos de Log](../../2014/integration-services/view-log-entries-in-the-log-events-window.md)  
  
  
