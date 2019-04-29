---
title: 'Lista de verificação de implantação: Expansão adicionando servidores do PowerPivot a um farm do SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 7bef5104038dad251927c6afff613f248f4a6a47
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "63025699"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>Lista de verificação de implantação: Expandir adicionando servidores do PowerPivot a um farm do SharePoint 2010
  Se você antecipar um alto volume de solicitações para o processamento de consultas PowerPivot em um farm do SharePoint, poderá adicionar uma instância extra do PowerPivot para SharePoint para adicionar diretamente o suporte para a nova consulta e o processamento de dados.  
  
 Depois que instalar uma nova instância, você terá capacidade adicional para consultar dados PowerPivot ou processar trabalhos de atualização de dados PowerPivot. Opcionalmente, você poderá configurar cada servidor para manipular um tipo de solicitação: consulta ou atualização de dados.  
  
## <a name="prerequisites"></a>Prerequisites  
 O SharePoint Server 2010 está instalado e configurado.  
  
 O SharePoint Server 2010 SP1 foi aplicado e o farm foi atualizado.  
  
 A instância do PowerPivot para SharePoint no farm é [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] (quer seja uma instalação nova ou atualizada do SQL Server 2008 R2).  
  
 O computador no qual você está instalando o novo [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] PowerPivot para SharePoint Server ingressa no farm. O computador e os outros servidores no farm devem estar no mesmo domínio.  
  
 Analise os tópicos adicionais a seguir para entender os requisitos de sistema e de versão:  
  
-   [Orientação para usar os recursos de BI do SQL Server em um farm do SharePoint 2010](../../../2014/sql-server/install/guidance-for-using-sql-server-bi-features-in-a-sharepoint-2010-farm.md)  
  
> [!NOTE]  
>  Em um farm multisservidor, todas as instâncias do PowerPivot para SharePoint devem estar na mesma versão. Se você aplicou service packs ou atualizações a outros servidores do PowerPivot que já estão no farm, a nova instância sendo adicionada deverá ser atualizada para a mesma versão da instância existente que já está no farm. A nova instância ficará indisponível até que as atualizações tenham sido aplicadas.  
  
## <a name="steps"></a>Etapas  
 Use esta lista de verificação para adicionar mais servidores do PowerPivot a um farm do SharePoint. Essas instruções pressupõem que você já tem um servidor do PowerPivot para SharePoint no farm, e que está adicionando um segundo servidor para tratar a carga de processamento adicional. Com exceção de diferenças em requisitos de instalação, configuração e verificação pós-instalação, as etapas para implantar uma solução em expansão são idênticas à adição de um único servidor do PowerPivot a um farm existente.  
  
|Etapa|Link|  
|----------|----------|  
|Determinar a conta de serviço da instância do Analysis Services que já está no farm|Cada instância adicional que você instala deve ser executada na mesma conta da primeira instância. Use uma das abordagens para determinar a conta de serviço:<br /><br /> Na Administração Central, na seção segurança, clique em **configurar contas de serviço**. Selecione **serviço do Windows – SQL Server Analysis Services**. Depois que você selecionar o serviço, o nome da conta do serviço aparecerá na página.<br /><br /> Em um servidor que já tenha uma instalação do serviço PowerPivot, abra o **Services** console aplicativo em Ferramentas administrativas. Clique duas vezes em **SQL Server Analysis Services**. Clique o **fazer logon** guia para exibir a conta de serviço.<br />**\*\* Importante \* \***  apenas usar a Administração Central para alterar contas de serviço. Se você usar outra ferramenta ou abordagem, as permissões não serão atualizadas corretamente no farm.|  
|Executar a Instalação para instalar uma segunda instância do PowerPivot para SharePoint|[Instalar o PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Escolha um servidor de aplicativo que tenha ingressado no farm, mas não tenha uma instância existente do PowerPivot no servidor.<br /><br /> Durante a Instalação, quando solicitado a especificar uma conta de serviço, insira a conta da etapa anterior. Todas as instâncias do serviço Analysis Services devem ser executadas na mesma conta de domínio. Esse requisito habilita o uso do recurso de contas gerenciadas no SharePoint que permite a você atualizar a senha em um local para todas as instâncias de serviço do mesmo tipo.|  
|Configurar a segunda instância|Você pode usar qualquer uma das abordagens para a configuração da instância: [Ferramentas de configuração do PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools.md) ou [configuração do PowerPivot usando o Windows PowerShell](../../analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell.md)<br /><br /> Ao configurar uma segunda instância, você só precisa provisionar os serviços locais. Todas as outras tarefas de configuração (como criar aplicativos de serviço ou configurar a atualização de dados) são executadas durante a configuração inicial e usadas pelas instâncias subsequentes que você instalar.|  
|Tarefas pós-instalação|Nenhuma outra etapa é especificamente necessária. Você não precisa criar aplicativos de serviço, ativar recursos, implantar soluções ou alterar a identidade de aplicativo de serviço. Aplicativos Web e aplicativos de serviço existentes descobrirão e usarão o novo software de servidor automaticamente.<br /><br /> Opcionalmente, se você instalou um segundo servidor para o propósito de usar um servidor para consultas e um para atualização de dados, poderá configurar propriedades de instância de serviço agora para especificar o tipo de solicitação manipulado por cada servidor. Para obter mais informações, consulte [configurar dedicado de atualização de dados ou processamento Query-Only &#40;PowerPivot para SharePoint&#41;](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).|  
|Verificar a instalação da segunda instância|Você pode usar as etapas a seguir para verificar o processamento de consulta PowerPivot no servidor que acabou de instalar.<br /><br /> 1) na Administração Central, abra gerenciar serviços na página de servidor para confirmar que o servidor e seus serviços aparecem.<br />-No servidor, clique na seta para baixo, clique em alterar servidor e, em seguida, selecione o servidor que tem a nova instalação do PowerPivot para SharePoint.<br />-Verifique se o SQL Server Analysis Services e o serviço de sistema do SQL Server PowerPivot foram iniciados.<br /><br /> 2) na Administração Central, interrompa outro servidores PowerPivot para SharePoint para que o servidor que você acabou de instalar é o único disponível. Para obter mais informações, consulte [iniciar ou parar um PowerPivot para SharePoint Server](../../analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server.md).<br /><br /> 3) clique em uma pasta de trabalho do PowerPivot para abri-lo da biblioteca.<br /><br /> 4) clique em uma segmentação de dados ou os dados para iniciar uma consulta de tabela dinâmica. O servidor carregará dados do PowerPivot em segundo plano. Na próxima etapa, você se conectará ao servidor para verificar se os dados foram carregados e armazenados em cache.<br /><br /> 5) iniciar o SQL Server Management Studio no grupo de programas Microsoft SQL Server no menu Iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.<br /><br /> 6) no tipo de servidor, selecione **Analysis Services**.<br /><br /> 7) no nome do servidor, insira  **\<server-name > \powerpivot.**, onde  **\<nome do servidor >** é o nome do computador que tem a nova instalação do PowerPivot para SharePoint.<br /><br /> 8) clique em **conectar-se**.<br /><br /> 9) no Pesquisador de objetos, clique em **bancos de dados** para exibir a lista de arquivos de dados do PowerPivot que são carregados.<br /><br /> 10) no sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos são armazenados no cache em disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivo, vá até a pasta \Arquivos de Programas\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup.<br /><br /> 11) reinicie os serviços antes interrompidos.|  
  
## <a name="see-also"></a>Consulte também  
 [Iniciais de configuração &#40;PowerPivot para SharePoint&#41;](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Administração e configuração de servidor do PowerPivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
