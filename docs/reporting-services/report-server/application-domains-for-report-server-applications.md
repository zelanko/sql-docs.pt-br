---
title: "Domínios de aplicativo para aplicativos de servidor de relatório | Microsoft Docs"
ms.custom: 
ms.date: 03/20/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- reporting-services-sharepoint
- reporting-services-native
ms.tgt_pltfrm: 
ms.topic: article
helpviewer_keywords:
- application domains [Reporting Services]
- recycling application domains
ms.assetid: a455e2e6-8764-493d-a1bc-abe80829f543
caps.latest.revision: 18
author: guyinacube
ms.author: asaxton
manager: erikre
ms.translationtype: HT
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 0cec89b68c69b5e5ae6875d5d5d5e721008844cd
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="application-domains-for-report-server-applications"></a>Domínios do aplicativo para aplicativos do Servidor de Relatório
  No [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], o servidor de relatório é implementado como um único serviço que contém um serviço Web Servidor de Relatórios, Gerenciador de Relatórios e um aplicativo executado em segundo plano. Cada aplicativo é executado em seu próprio domínio de aplicativo dentro do único processo de servidor de relatório. Para a maior parte, os domínios de aplicativo são criados, configurados e gerenciados internamente. Entretanto, saber como as operações de reciclagem ocorrem para os domínios de aplicativo para servidores de relatório poderá ser útil se você estiver investigando o desempenho ou problemas de memória ou solucionando problemas de interrupção de serviço.  
  
> [!NOTE]  
>  Se você configurar o acesso ao Construtor de Relatórios em um servidor de relatório que usa autenticação Básica, ele executará seu próprio domínio de aplicativo. Esse domínio é diferente de outros domínios de aplicativo que são executados no processo de servidor. Ele é gerenciado pelo Controlador de Serviço e não está sujeito aos recursos de gerenciamento de memória que reajustam a alocação em resposta à pressão de memória no servidor de relatório.  
  
 A seguinte lista descreve os eventos que causam operações de reciclagem de domínio para aplicativos [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] :  
  
-   Operações de reciclagem programadas que ocorrem em intervalos predefinidos.  
  
-   Alterações de configuração no servidor de relatório.  
  
-   Alterações de configuração [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)].  
  
-   Falhas de alocação de memória.  
  
 A seguinte tabela resume o domínio de aplicativo que recicla comportamento em resposta a esses eventos:  
  
|Evento|Descrição do evento|Aplica-se a|Configurável|Descrição de operação de reciclagem|  
|-----------|-----------------------|----------------|------------------|-----------------------------------|  
|Operações de reciclagem programadas que ocorrem em intervalos predefinidos|Por padrão, os domínios de aplicativo são reciclados a cada 12 horas.<br /><br /> As operações de reciclagem programadas são práticas comuns para aplicativos do [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] que promovem a integridade do processo geral.|Serviço Web Servidor de Relatórios<br /><br /> Gerenciador de Relatórios<br /><br /> Aplicativo de processamento em segundo plano|Sim. A definição de configuração**RecycleTime** no arquivo RSReportServer.config determina o intervalo de reciclagem.<br /><br /> **MaxAppDomainUnloadTime** define o tempo de espera durante o qual o processamento em segundo plano pode ser concluído.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] gerencia a operação de reciclagem para o serviço Web e o Gerenciador de Relatórios.<br /><br /> Para o aplicativo de processamento em segundo plano, o servidor de relatório cria um novo domínio de aplicativo para novos trabalhos iniciados pelas agendas. Os trabalhos já em progresso podem ser concluídos no domínio de aplicativo atual até que o tempo de espera expire.|  
|Alterações de configuração no servidor de relatório.|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] reciclará domínios de aplicativo em resposta a alterações no arquivo RSReportServer.config.|Serviço Web Servidor de Relatórios<br /><br /> Gerenciador de Relatórios<br /><br /> Aplicativo de processamento em segundo plano|Nenhum.|Você não pode impedir que as operações de reciclagem aconteçam. Entretanto, as operações de reciclagem que ocorrem em resposta a alterações de configuração são tratadas da mesma maneira que operações de reciclagem programadas. Novos domínios de aplicativo são criados para novas solicitações enquanto solicitações atuais e trabalhos são concluídos no domínio de aplicativo atual.|  
|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] alterações de configuração|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]reciclará domínios de aplicativo se houver alterações nos arquivos monitorados (por exemplo, Machine. config e arquivos Web. config, e [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] arquivos de programa).|Serviço Web Servidor de Relatórios<br /><br /> Gerenciador de Relatórios|Nenhum.|[!INCLUDE[vstecasp](../../includes/vstecasp-md.md)]gerencia a operação.<br /><br /> As operações de reciclagem iniciadas por [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] não afetam o domínio de aplicativo de processamento em segundo plano.|  
|Pressão de memória e falhas de alocação de memória|A CLR do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] reciclará imediatamente domínios de aplicativo no caso de uma falha de alocação de memória ou quando o servidor estiver sob condições de alta pressão de memória.|Serviço Web Servidor de Relatórios<br /><br /> Gerenciador de Relatórios<br /><br /> Aplicativo de processamento em segundo plano|Nenhum.|Sob alta pressão de memória, o servidor de relatório não aceitará novas solicitações no domínio de aplicativo atual. Durante o período no qual o servidor nega novas solicitações, ocorrem erros HTTP 503. Não serão criados novos domínios de aplicativo até que o antigo domínio de aplicativo seja descarregado. Isso significa que, se você alterar o arquivo de configuração enquanto o servidor estiver sob alta pressão de memória, solicitações e trabalhos em progresso poderão não ser iniciados ou concluídos.<br /><br /> No caso de falha de alocação de memória, todos os domínios de aplicativo serão reinicializados imediatamente. Trabalhos e solicitações que estejam em progresso serão descartados. Você deve reinicializar esses trabalhos e solicitações manualmente.|  
  
## <a name="planned-and-unplanned-recycle-operations"></a>Operações de reciclagem planejadas e não planejadas  
 As operações de reciclagem planejadas ou não planejadas dependem das condições que acompanham a operação:  
  
-   As operações de reciclagem planejadas ocorrem em intervalos regulares definidos no arquivo RSReportServer.config. O padrão é a cada 12 horas. Essa é uma prática comum para aplicativos [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] que promovem a integridade do processo geral. Para operações de reciclagem planejadas, o servidor de relatório cria domínios de aplicativo adicionais para novas solicitações. As solicitações já em progresso podem ser concluídas no domínio de aplicativo atual até que o tempo de espera expire. As definições de configuração que governam as operações de reciclagem planejadas são definidas para o servidor como um todo. Você não pode configurar uma agenda de reciclagem diferente ou limite de memória para cada aplicativo.  
  
-   As operações e reciclagem não planejadas ocorrem em períodos arbitrários em resposta a alterações de configuração, pressão de memória e falhas de alocação de memória:  
  
    -   Nas alterações de configuração, o servidor de relatório tentará usar uma reciclagem suave que redireciona novas solicitações a uma nova instância do domínio de aplicativo. Se a reciclagem suave falhar, o servidor iniciará uma reciclagem de domínio de aplicativo agressiva que cancela todas as solicitações em progresso, desliga os domínios de aplicativo atuais e reinicia os domínios de aplicativo.  
  
    -   As falhas de alocação de memória indicam que os recursos do sistema não são suficientes para a quantidade de processamento de relatório executada pelo servidor. Uma operação de reciclagem agressiva de todos os domínios de aplicativo ocorre em resposta a uma falha de alocação de memória. Todas as filas de solicitação são desmarcadas. As solicitações canceladas não são reinicializadas. Usuários que exibiam um relatório interativamente devem atualizar ou reabrir o relatório. O processamento programado ocorrerá no próximo período programado. Se o atraso for inaceitável, você poderá atualizar um instantâneo de relatório manualmente ou modificar uma agenda de assinatura ou agenda de instantâneo de relatório de modo a ser executada imediatamente.  
  
 Os domínios de aplicativo para o serviço Web Servidor de Relatórios, Gerenciador de Relatórios e o aplicativo de processamento de segundo plano podem ser reciclados juntos ou individualmente, dependendo das circunstâncias que provocam a reciclagem.  
  
-   As operações de reciclagem iniciadas pelo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] afetam apenas os aplicativos do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] : Serviço Web Servidor de Relatórios e Gerenciador de Relatórios. O [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] reciclará domínios do aplicativo com base em alterações nos arquivos que monitora. As operações de reciclagem iniciadas por [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] são tipicamente independentes das operações de reciclagem do aplicativo de processamento em segundo plano.  
  
-   As operações de reciclagem iniciadas pelo servidor de relatório geralmente afetam o serviço Web Servidor de Relatórios, o Gerenciador de Relatórios e o aplicativo processado em segundo plano. As operações de reciclagem ocorrem em resposta a alterações nas definições de configuração e o serviço é reinicializado.  
  
## <a name="rsreportserver-configuration-settings-for-application-domains"></a>Definições de configuração RSReportServer para domínios de aplicativo  
 As definições de configuração são especificadas no [arquivo RSReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md). O exemplo a seguir mostra as definições de configuração padrão para o comportamento de reciclagem de domínio de aplicativo.  
  
 `<RecycleTime>720</RecycleTime>`  
  
 `<MaxAppDomainUnloadTime>30</MaxAppDomainUnloadTime>`  
  
 A tabela a seguir descreve esses elementos.  
  
|Elemento|Aplica-se a|Definição|  
|-------------|----------------|----------------|  
|**RecycleTime**|Todos os três domínios de aplicativo [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]|Especifica com que frequência os domínios de aplicativo são reciclados. A agenda de reciclagem padrão está em conformidade com o padrão de 12 horas geralmente seguido pela reciclagem de domínio de aplicativo [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] . No momento marcado, todas as novas solicitações são encaminhadas a uma nova instância do domínio de aplicativo. As solicitações atualmente em progresso na instância original podem ser concluídas. Após todos os processos terem sido concluídos, a instância original é excluída e a nova instância torna-se a única instância de domínio de aplicativo ativa.<br /><br /> O valor padrão é de 720 minutos.|  
|**MaxAppDomainUnloadTime**|Apenas ao domínio de aplicativo de processamento em segundo plano|Por padrão, um servidor de relatório aloca um tempo de espera de 30 minutos, durante o qual um domínio de aplicativo pode ser desligado durante a operação de reciclagem. Se os trabalhos atualmente em processo não puderem ser concluídos durante o período alocado (ou se um trabalho estiver demorando mais do que o tempo de espera permitido), a instância de domínio de aplicativo será reinicializada imediatamente. Todos os trabalhos incompletos são encerrados.<br /><br /> Para obter mais informações sobre como exibir status ou cancelar trabalhos sendo executados no servidor de relatório, consulte [Cancelar Trabalhos do Servidor de Relatório &#40;Management Studio&#41;](../../reporting-services/tools/cancel-report-server-jobs-management-studio.md).|  
  
> [!NOTE]  
>  Apesar de o serviço Web Servidor de Relatórios e o Gerenciador de Relatórios serem aplicativos [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)], nenhum responde à reciclagem de domínio de aplicativo programada que pode ser especificada em machine.config por aplicativos [!INCLUDE[vstecasp](../../includes/vstecasp-md.md)] hospedados em IIS.  
  
## <a name="see-also"></a>Consulte também  
 [Arquivo de Configuração RsReportServer.config](../../reporting-services/report-server/rsreportserver-config-configuration-file.md)   
 [Modificar um arquivo de configuração do Reporting Services &#40; Rsreportserver. config &#41;](../../reporting-services/report-server/modify-a-reporting-services-configuration-file-rsreportserver-config.md)   
 [Configurar a memória disponível para aplicativos de servidor de relatório](../../reporting-services/report-server/configure-available-memory-for-report-server-applications.md)  
  
  
