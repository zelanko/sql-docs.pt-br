---
title: "Adicionar um log para contadores de desempenho de fluxo de dados | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "contadores de desempenho [Integration Services]"
  - "contadores [Integration Services]"
  - "logs [Integration Services], contadores de fluxo de dados"
ms.assetid: b500d166-33ba-4b82-a92d-b0a333924e8d
caps.latest.revision: 25
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 25
---
# Adicionar um log para contadores de desempenho de fluxo de dados
  Este procedimento descreve como adicionar um log para os contadores de desempenho fornecidos pelo mecanismo de fluxo de dados.  
  
> [!NOTE]  
>  Se você instalar o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] em um computador que está executando o [!INCLUDE[winxpsvr](../../includes/winxpsvr-md.md)]e, em seguida, atualizar o computador para o [!INCLUDE[firstref_longhorn](../../includes/firstref-longhorn-md.md)], o processo de atualização removerá os contadores de desempenho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] do computador. Para restaurar os contadores de desempenho do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no computador, execute a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em modo de reparo.  
  
### Para adicionar registros de contadores de desempenho  
  
1.  No **Painel de Controle**, se você estiver usando a exibição Clássica, clique em **Ferramentas Administrativas**. Se você estiver usando a exibição Categoria, clique em **Desempenho e Manutenção** e clique em **Ferramentas Administrativas**.  
  
2.  Clique em **Desempenho**.  
  
3.  Na caixa de diálogo **Desempenho**, expanda **Logs e Alertas de Desempenho**, clique com o botão direito do mouse em **Logs do Contador** e clique em **Novas Configurações de Log**. Digite o nome do log. Por exemplo, digite **MyLog**.  
  
4.  Clique em **OK**.  
  
5.  Na caixa de diálogo **MyLog**, clique em **Adicionar Contadores**.  
  
6.  Clique em **Usar contadores locais do computador** para registrar contadores de desempenho no computador local ou clique em **Selecionar contadores do computador** e selecione um computador da lista para registrar os contadores de desempenho no computador especificado.  
  
7.  Na caixa de diálogo **Adicionar contadores**, selecione **SQL Server:SSIS Pipeline** na lista **Objeto de desempenho**.  
  
8.  Para selecionar contadores de desempenho, execute um dos seguintes procedimentos:  
  
    -   Selecione **Todos os contadores** para registrar todos os contadores de desempenho.  
  
    -   Selecione **Selecionar contadores na lista** e selecione o contador de desempenho a ser usado.  
  
9. Clique em **Adicionar**.  
  
10. Clique em **Fechar**.  
  
11. Na caixa de diálogo **MyLog**, examine a lista de registro de contadores de desempenho na lista **Contadores**.  
  
12. Para adicionar contadores extras, repitas as etapas de 5 a 10.  
  
13. Clique em **OK**.  
  
    > [!NOTE]  
    >  Você deve iniciar o serviço Logs e Alertas de Desempenho usando uma conta local ou uma conta de domínio que seja um membro do grupo Administradores.  
  
## Consulte também  
 [Contadores de desempenho](../../integration-services/performance/performance-counters.md)   
 [Exibir entradas de log na janela Eventos de Log](../../integration-services/performance/view-log-entries-in-the-log-events-window.md)  
  
  