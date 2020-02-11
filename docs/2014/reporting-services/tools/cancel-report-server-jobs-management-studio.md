---
title: Cancelar Trabalhos do Servidor de Relatório (Management Studio) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.cancelreportserverjobs.f1
ms.assetid: 1c5b4975-49e9-4d0b-b298-2638e81edbfd
author: maggiesMSFT
ms.author: maggies
manager: kfile
ms.openlocfilehash: ab7c4496465de8297f07dd18b3aa2acf26ab305d
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66100497"
---
# <a name="cancel-report-server-jobs-management-studio"></a>Cancelar Trabalhos do Servidor de Relatório (Management Studio)
  Use a caixa de diálogo **Cancelar Trabalhos do Servidor de Relatório** para exibir ou cancelar relatórios em andamento. Essa caixa de diálogo mostra todos os trabalhos em execução atualmente no servidor de relatórios. Embora você não possa pausar ou reiniciar trabalhos atualmente em processo, pode cancelar todos os trabalhos ou trabalhos individuais se estiverem demorando muito para serem concluídos.  
  
 Você pode cancelar trabalhos de usuário e trabalhos do sistema.  
  
-   Um trabalho de usuário é qualquer trabalho iniciado por um usuário individual. Isso inclui a execução de um relatório sob demanda, a criação manual de um instantâneo de histórico de relatório ou de um instantâneo de execução de relatório. Uma assinatura padrão em andamento é também um trabalho de usuário.  
  
-   Um trabalho do sistema é um trabalho iniciado pelo servidor de relatórios. Trabalhos do sistema incluem processamento de relatório agendado.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a um servidor de relatório, clique com o botão direito do mouse em **Trabalhos**e clique em **Cancelar Todos os Trabalhos**. Você pode abrir também **Trabalhos**, clicar com o botão direito do mouse em um trabalho em execução no servidor de relatório e selecionar **Cancelar Trabalho(s)** .  
  
 Antes de cancelar um trabalho, você pode exibir suas propriedades para determinar quando o trabalho foi iniciado. Para obter mais informações, consulte [Propriedades do Trabalho &#40;Management Studio&#41;](job-properties-management-studio.md).  
  
> [!NOTE]  
>  Esse recurso não tem suporte no [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)] com Advanced Services. A página não será exibida enquanto você estiver executando o [!INCLUDE[ssExpress](../../includes/ssexpress-md.md)].  
  
## <a name="options"></a>Opções  
 **Nome**  
 Exibe o nome do relatório. As assinaturas são identificadas por suas descrições.  
  
 **Tipo**  
 Os valores válidos são **User** e **System**.  
  
 **Start Time**  
 Exibe quando o trabalho foi iniciado.  
  
 **Nome de usuário**  
 Para trabalhos iniciados por um usuário, essa coluna exibe o nome do usuário.  
  
 **Status**  
 Mostra o status atual do trabalho. Os valores válidos são **Novo** e **Executando**. O status é sempre **Novo** quando o trabalho começa. Depois de 60 segundos, o status é alterado para **Executando**. É necessário atualizar a página para que a alteração tenha efeito.  
  
 **OK**  
 Cancele um único trabalho ou vários trabalhos. Os trabalhos são imediatamente cancelados e não podem ser retomados. Se você cancelar um trabalho por engano, deverá solicitar o relatório ou a assinatura novamente para iniciar um novo trabalho.  
  
## <a name="see-also"></a>Consulte Também  
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Gerenciar um processo em execução](../subscriptions/manage-a-running-process.md)  
  
  
