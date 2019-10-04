---
title: 'Lista de verificação de implantação: Escalar horizontalmente adicionando servidores PowerPivot a um farm do SharePoint 2010 | Microsoft Docs'
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 2dbddcc7-427a-4537-a8e2-56d99b9d967d
author: maggiesMSFT
ms.author: maggies
manager: craigg
ms.openlocfilehash: d3a5fab0a0502d2e6faba2f66b64ae65b995b48f
ms.sourcegitcommit: ffe2fa1b22e6040cdbd8544fb5a3083eed3be852
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/04/2019
ms.locfileid: "71952181"
---
# <a name="deployment-checklist-scale-out-by-adding-powerpivot-servers-to-a-sharepoint-2010-farm"></a>Lista de verificação de implantação: Expandir adicionando servidores do PowerPivot a um farm do SharePoint 2010
  Se você antecipar um alto volume de solicitações para o processamento de consultas PowerPivot em um farm do SharePoint, poderá adicionar uma instância extra do PowerPivot para SharePoint para adicionar diretamente o suporte para a nova consulta e o processamento de dados.  
  
 Depois que instalar uma nova instância, você terá capacidade adicional para consultar dados PowerPivot ou processar trabalhos de atualização de dados PowerPivot. Opcionalmente, você poderá configurar cada servidor para manipular um tipo de solicitação: consulta ou atualização de dados.  
  
## <a name="prerequisites"></a>Pré-requisitos  
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
|Determinar a conta de serviço da instância do Analysis Services que já está no farm|Cada instância adicional que você instala deve ser executada na mesma conta da primeira instância. Use uma das abordagens para determinar a conta de serviço:<br /><br /> Na administração central, na seção segurança, clique em **Configurar contas de serviço**. Selecione **serviço do Windows-SQL Server Analysis Services**. Depois que você selecionar o serviço, o nome da conta do serviço aparecerá na página.<br /><br /> Em um servidor que já tenha uma instalação de serviço PowerPivot, abra o aplicativo de console **Serviços** em ferramentas administrativas. Clique duas vezes em **SQL Server Analysis Services**. Clique na guia **fazer logon** para exibir a conta de serviço.<br />**\* @ no__t-2 importante \* @ no__t-4** Use a administração central somente para alterar as contas de serviço. Se você usar outra ferramenta ou abordagem, as permissões não serão atualizadas corretamente no farm.|  
|Executar a Instalação para instalar uma segunda instância do PowerPivot para SharePoint|[Instalar o PowerPivot para SharePoint 2010](../../../2014/sql-server/install/install-powerpivot-for-sharepoint-2010.md)<br /><br /> Escolha um servidor de aplicativo que tenha ingressado no farm, mas não tenha uma instância existente do PowerPivot no servidor.<br /><br /> Durante a Instalação, quando solicitado a especificar uma conta de serviço, insira a conta da etapa anterior. Todas as instâncias do serviço Analysis Services devem ser executadas na mesma conta de domínio. Esse requisito habilita o uso do recurso de contas gerenciadas no SharePoint que permite a você atualizar a senha em um local para todas as instâncias de serviço do mesmo tipo.|  
|Configurar a segunda instância|Você pode usar qualquer uma das abordagens para configurar a instância: Configuração do PowerPivot [ferramentas de configuração](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-tools) ou do [PowerPivot usando o Windows PowerShell](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-configuration-using-windows-powershell)<br /><br /> Ao configurar uma segunda instância, você só precisa provisionar os serviços locais. Todas as outras tarefas de configuração (como criar aplicativos de serviço ou configurar a atualização de dados) são executadas durante a configuração inicial e usadas pelas instâncias subsequentes que você instalar.|  
|Tarefas de pós-instalação|Nenhuma outra etapa é especificamente necessária. Você não precisa criar aplicativos de serviço, ativar recursos, implantar soluções ou alterar a identidade de aplicativo de serviço. Aplicativos Web e aplicativos de serviço existentes descobrirão e usarão o novo software de servidor automaticamente.<br /><br /> Opcionalmente, se você instalou um segundo servidor para o propósito de usar um servidor para consultas e um para atualização de dados, poderá configurar propriedades de instância de serviço agora para especificar o tipo de solicitação manipulado por cada servidor. Para obter mais informações, consulte [Configurar a atualização de dados dedicada ou processamento &#40;somente&#41;de consulta PowerPivot para SharePoint](../../analysis-services/configure-dedicated-data-refresh-query-only-processing-powerpivot-sharepoint.md).|  
|Verificar a instalação da segunda instância|Você pode usar as etapas a seguir para verificar o processamento de consulta PowerPivot no servidor que acabou de instalar.<br /><br /> 1) na administração central, abra a página gerenciar serviços no servidor para confirmar se o servidor e seus serviços são exibidos.<br />No servidor, clique na seta para baixo, clique em alterar servidor e selecione o servidor que tem a nova instalação do PowerPivot para SharePoint.<br />-Verifique se as Serviço de Sistema PowerPivot de SQL Server Analysis Services e SQL Server foram iniciadas.<br /><br /> 2) na administração central, interrompa outros servidores PowerPivot para SharePoint para que o servidor que você acabou de instalar seja o único disponível. Para obter mais informações, consulte [Iniciar ou parar um servidor de PowerPivot para SharePoint](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/start-or-stop-a-power-pivot-for-sharepoint-server).<br /><br /> 3) clique em uma pasta de trabalho PowerPivot para abri-la da biblioteca.<br /><br /> 4) clique em uma segmentação ou dinamizar os dados para iniciar uma consulta. O servidor carregará dados do PowerPivot em segundo plano. Na próxima etapa, você se conectará ao servidor para verificar se os dados foram carregados e armazenados em cache.<br /><br /> 5) inicie o SQL Server Management Studio no grupo de programas Microsoft SQL Server no menu iniciar. Se essa ferramenta não estiver instalada no servidor, será possível passar à última etapa para confirmar a presença de arquivos armazenados em cache.<br /><br /> 6) em tipo de servidor, selecione **Analysis Services**.<br /><br /> 7) em nome do servidor, digite **\<server-nome > \powerpivot**, em que **\<server-Name >** é o nome do computador que tem a nova instalação do PowerPivot para SharePoint.<br /><br /> 8) clique em **conectar**.<br /><br /> 9) no Pesquisador de objetos, clique em **bancos** de dados para exibir a lista de arquivos de dados PowerPivot que são carregados.<br /><br /> 10) no sistema de arquivos do computador, verifique a pasta a seguir para determinar se os arquivos são armazenados em cache no disco. A presença de arquivos armazenados em cache é a verificação adicional de que a implantação é operacional. Para exibir o cache de arquivo, vá até a pasta \Arquivos de Programas\Microsoft SQL Server\MSAS11.POWERPIVOT\OLAP\Backup.<br /><br /> 11) reinicie os serviços que você interrompeu anteriormente.|  
  
## <a name="see-also"></a>Consulte também  
 [&#41;PowerPivot para SharePoint de &#40;configuração inicial](../../../2014/sql-server/install/initial-configuration-powerpivot-for-sharepoint.md)   
 [Instalação do PowerPivot para SharePoint 2010](../../../2014/sql-server/install/powerpivot-for-sharepoint-2010-installation.md)   
 [Administração e configuração de servidor do PowerPivot na Administração Central](https://docs.microsoft.com/analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration)  
  
  
