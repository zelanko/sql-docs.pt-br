---
title: Propriedades de Trabalho (Management Studio) | Microsoft Docs
ms.date: 03/01/2017
ms.prod: reporting-services
ms.prod_service: reporting-services-sharepoint, reporting-services-native
ms.technology: tools
ms.suite: pro-bi
ms.topic: conceptual
f1_keywords:
- sql13.swb.reportserver.jobproperties.f1
ms.assetid: 807ffd0e-9363-4f8f-9c36-c5d746ad19fd
author: markingmyname
ms.author: maghan
ms.openlocfilehash: 1a5f23a8251790cedc36b5991f75e658d67257e7
ms.sourcegitcommit: d96b94c60d88340224371926f283200496a5ca64
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/30/2018
ms.locfileid: "43264705"
---
# <a name="job-properties-management-studio"></a>Propriedades do Trabalho (Management Studio)
  Use a página **Propriedades do Trabalho** para exibir informações sobre um relatório ou uma assinatura em andamento antes de serem cancelados.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a um servidor de relatórios e abra a pasta **Trabalhos** . Clique com o botão direito do mouse em um trabalho em execução e clique em **Propriedades**.  
  
> [!NOTE]  
>  Esse recurso não tem suporte no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] com Advanced Services. A página não será exibida enquanto você estiver executando o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
## <a name="tasks"></a>Tarefas  
 Antes de exibir informações sobre um trabalho, atualize a página para recuperar informações sobre trabalhos atualmente em execução no servidor de relatórios:  
  
1.  Abra a pasta do servidor de relatórios.  
  
2.  Clique com o botão direito do mouse em **Trabalhos**e clique em **Atualizar**.  
  
3.  Se um trabalho estiver listado, clique com o botão direito do mouse no trabalho e depois clique em **Propriedades**.  
  
## <a name="options"></a>Opções  
 **ID do Trabalho**  
 Um GUID atribuído a um trabalho durante o processamento. O valor é gerado aleatoriamente cada vez que um relatório ou uma assinatura é executado.  
  
 **Status do Trabalho**  
 Os valores válidos são **Novo** e **Executando**. O status é sempre **Novo** quando o trabalho começa. Depois de 60 segundos, o status é alterado para **Executando**. É necessário atualizar a página para que a alteração tenha efeito.  
  
 **Tipo de Trabalho**  
 Os valores válidos são **User** e **System**. Um trabalho de usuário é qualquer trabalho iniciado por um usuário individual. Isso inclui a execução de um relatório sob demanda, a geração manual de um instantâneo de histórico de relatório ou de um instantâneo de execução de relatório. Uma assinatura padrão em andamento é também um trabalho de usuário. Um trabalho do sistema é um trabalho iniciado pelo servidor de relatórios. Trabalhos do Sistema incluem processamento de relatório que é disparado por uma agenda.  
  
 **Ação do Trabalho**  
 Para relatórios, esta coluna mostra quais processos de execução de relatório estão a caminho. Esse valor sempre é **Renderizar**.  
  
 **Descrição do Trabalho**  
 O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] não fornece descrições de trabalho por padrão.  
  
 **Nome do servidor**  
 Exibe o nome do servidor de relatórios que está processando o trabalho. Se você configurou uma implantação em expansão, esse valor mostrará qual servidor está processando o trabalho.  
  
 **Nome do Relatório**  
 Exibe o nome do relatório. As assinaturas são identificadas por suas descrições.  
  
 **Caminho do Relatório**  
 Exibe o caminho do relatório na hierarquia de pastas do servidor de relatórios.  
  
 **Start Time**  
 Exibe quando o processo foi iniciado.  
  
 **Nome do Usuário**  
 Para processos iniciados por um usuário, essa coluna mostra o nome do usuário. Para trabalhos do sistema, este é o nome do servidor de relatórios.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](../../reporting-services/tools/report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](../../reporting-services/tools/connect-to-a-report-server-in-management-studio.md)   
 [Gerenciar um processo em execução](../../reporting-services/subscriptions/manage-a-running-process.md)  
  
  
