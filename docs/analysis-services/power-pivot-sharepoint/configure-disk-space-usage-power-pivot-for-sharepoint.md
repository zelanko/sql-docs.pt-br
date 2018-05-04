---
title: Configurar o uso de espaço em disco (PowerPivot para SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: article
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: 7388a8f44b3dc60729674a6cd14014d4bbfa15f4
ms.sourcegitcommit: 2ddc0bfb3ce2f2b160e3638f1c2c237a898263f4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/03/2018
---
# <a name="configure-disk-space-usage-power-pivot-for-sharepoint"></a>Configurar o uso do espaço em disco (PowerPivot para SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Uma implantação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa o espaço em disco do computador host para armazenar em cache bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para agilizar as recargas. Todo banco de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que é carregado na memória é armazenado primeiro no disco para agilizar a recarga posterior para atender a novas solicitações. Por padrão, o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa todo o espaço em disco disponível para armazenar seus bancos de dados, mas pode modificar esse comportamento definindo propriedades que limitam a quantidade de espaço em disco utilizado.  
  
 Este tópico explica como definir os limites sobre o uso de espaço em disco.  
  
 Este tópico não fornece diretrizes para o gerenciamento de espaço em disco de bancos de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] (inseridos em pastas de trabalho do Excel) que são armazenados em bancos de dados de conteúdo. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] podem ser grandes, colocando assim novas exigências sobre a capacidade de armazenamento do farm. Além disso, se o controle de versão estiver habilitado, você poderá perfeitamente ter várias cópias dos dados no mesmo banco de dados de conteúdo, aumentando mais a quantidade de espaço necessário em disco para o armazenamento de conteúdo. Embora bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] sejam uma consideração importante no gerenciamento de disco, eles não podem ser gerenciados independentemente de outro conteúdo armazenado em um farm do SharePoint. Você precisará monitorar ainda mais o espaço em disco à medida que seus negócios fizerem mais uso de pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Você também pode acompanhar a atividade de pastas de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e remover pastas de trabalho que não forem mais usadas.  
  
## <a name="how-power-pivot-for-sharepoint-manages-cached-databases"></a>Como o PowerPivot para SharePoint gerencia bancos de dados armazenados em cache  
 Para gerenciar seu cache, o serviço de sistema do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] executa um trabalho em segundo plano em intervalos regulares para limpar bancos de dados não usados ou desatualizados com versões mais recentes em uma biblioteca de conteúdo. O propósito do trabalho de limpeza é descarregar bancos de dados inativos da memória e excluir bancos de dados não usados, armazenados em cache do sistema de arquivos. O trabalho de limpeza é para manutenção de longo prazo, garantindo que bancos de dados não permaneçam no sistema por um tempo indefinido. Em um servidor ativo, talvez bancos de dados sejam removidos com mais frequência devido à pressão de memória no servidor, à exclusão de banco de dados no SharePoint ou a versões mais recentes do banco de dados em uma biblioteca de conteúdo.  
  
 Embora você não possa agendar o trabalho de limpeza, pode personalizar o gerenciamento de arquivo de cache definindo propriedades de configuração de servidor que fazem o seguinte:  
  
-   Definir limites na quantidade de espaço em disco usada pelo cache.  
  
-   Especificar o volume de dados a ser excluído quando o espaço máximo em disco é alcançado.  
  
## <a name="how-to-check-disk-space-usage"></a>Como verificar o uso do espaço em disco  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint é instalado em servidores de aplicativo um farm do SharePoint. Cada instalação tem um diretório de dados que inclui uma pasta Backup. A pasta Backup contém todos os arquivos de dados que são armazenados em cache pela instância do Analysis Services no computador. Por padrão, a pasta Backup pode ser localizada no seguinte caminho:  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 Para verificar o total de espaço em disco usado pelo cache, verifique o tamanho da pasta Backup. Não há propriedades na Administração Central com relatos sobre o tamanho de cache atual.  
  
 A pasta Backup oferece o armazenamento em cache comum para qualquer banco de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] carregado na memória no computador local. Se você tiver vários aplicativos de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] definidos no farm, qualquer um deles poderá usar o servidor local para carregar e subsequentemente armazenar em cache dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O carregamento e o armazenamento de dados em cache são operações de servidor do Analysis Services. Sendo assim, o uso total de espaço em disco é gerenciado em nível de instância do Analysis Services, na pasta Backup. Parâmetros de configuração que limitam o uso de espaço em disco são definidos na única instância do SQL Server Analysis Services que é executada em um servidor de aplicativos do SharePoint.  
  
 O cache contém apenas bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Os bancos de dados são armazenados em vários arquivos em uma única pasta pai (a pasta Backup). Como bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] devem ser usados como dados internos em uma pasta de trabalho do Excel, nomes de bancos de dados se baseiam em GUID, e não são descritivos. Uma pasta GUID em  **\<serviceApplicationName >** é a pasta pai de um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] banco de dados. Como os bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são carregados no servidor, pastas adicionais são criadas para cada um.  
  
 Como os dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] podem ser carregados em qualquer instância do Analysis Services em um farm, os mesmos dados também podem ser armazenados em cache em vários computadores no farm. Essa prática favorece o desempenho na utilização de espaço em disco, mas a compensação é que os usuários acessam dados mais rápido quando eles já estão disponíveis em disco.  
  
 Para reduzir imediatamente o consumo de espaço em disco, você pode desligar o serviço e, depois, excluir um banco de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] da pasta Backup. A exclusão manual de arquivos é uma medida temporária, pois uma cópia mais nova do banco de dados será armazenada em cache novamente da próxima vez que dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] forem consultados. Soluções permanentes incluem a limitação do espaço em disco usado pelo cache.  
  
 Em nível de sistema, você pode criar alertas de email que notifiquem quando o espaço em disco for baixo. O Microsoft System Center inclui um recurso de alerta de email. Você também pode usar o Gerenciador de Recursos do Servidor de Arquivo, o Agendador de Tarefas ou o script PowerShell para configurar alertas. Os links a seguir especificam informações úteis para configurar notificações sobre espaço em disco insuficiente:  
  
-   [O que há de novo no Gerenciador de recursos de servidor de arquivos](http://technet.microsoft.com/library/hh831746.aspx) (http://technet.microsoft.com/library/hh831746.aspx).  
  
-   [Guia passo a passo do Gerenciador de recursos de servidor de arquivos para Windows Server 2008 R2](http://go.microsoft.com/fwlink/?LinkID=204875) (http://go.microsoft.com/fwlink/?LinkID=204875).  
  
-   [Definindo alertas de espaço em disco insuficiente no Windows Server 2008](http://go.microsoft.com/fwlink/?LinkID=204870) ( http://go.microsoft.com/fwlink/?LinkID=204870).  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>Como limitar a quantidade de espaço em disco usada para armazenar arquivos em cache  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Serviços no Servidor**.  
  
2.  Clique **SQL Server Analysis Services**.  
  
     Note que os limites são definidos na instância do Analysis Services que é executada no servidor físico, e não em nível de aplicativo de serviço. Todos os aplicativos de serviço que usam a instância do Analysis Services local estão sujeitos ao único limite máximo de espaço em disco que é definido para essa instância.  
  
3.  Em Uso de Disco, defina um valor (em gigabytes) para **Total de espaço em disco** para definir um limite superior na quantidade de espaço usado para fins de cache. O padrão é 0, que permite ao Analysis Services usar todo o espaço disponível em disco.  
  
4.  Em Uso de Disco, na configuração **Excluir bancos de dados armazenados em cache nas últimas ‘n’ horas** , especifique os critérios usados por último para esvaziar o cache quando o espaço em disco atingir o limite máximo.  
  
     O padrão são 4 horas, o que significa que todos os bancos de dados que ficaram inativos por 4 horas ou mais serão excluídos do sistema de arquivos. Bancos de dados que estão inativos, mas que permanecem em memória, são descarregados e depois excluídos do sistema de arquivos.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>Como limitar o tempo de permanência de um banco de dados no cache  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique em **Aplicativo de Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Padrão** para abrir o painel de gerenciamento.  
  
3.  Em Ações, clique em **Definir configurações do aplicativo de serviço**.  
  
4.  Na seção Cache de Disco, você pode especificar quanto tempo um banco de dados permanece inativo em memória para atender novas solicitações (por padrão, 48 horas) e quanto tempo ele permanece no cache (por padrão, 120 horas).  
  
     **Mantenha Banco de dados Inativo em Memória** especifica quanto tempo um banco de dados inativo fica em memória para atender novas solicitações desses dados. Um banco de dados ativo sempre será mantido em memória contanto que você esteja consultando-o, mas depois ele não permanecerá ativo. O sistema manterá o banco de dados em memória por um período de tempo adicional caso existam mais solicitações desses dados.  
  
     Como os bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] primeiro são armazenados em cache e, depois, carregados em memória, os arquivos de banco de dados consomem espaço em disco imediatamente. Entretanto, apesar de o banco de dados estar ativo (e por 48 horas depois disso), todas as solicitações são direcionadas primeiro ao banco de dados em memória, ignorando o banco de dados em cache. Depois de 48 horas de inatividade, o arquivo é descarregado da memória, mas permanece no cache, no qual poderá ser recarregado rapidamente se uma nova solicitação de conexão desses dados for interceptada pela instância de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] local. As solicitações de conexão a um banco de dados inativo são atendidas do cache e não da biblioteca de conteúdo, minimizando o impacto nos bancos de dados de conteúdo.  
  
     É importante observar que a biblioteca de conteúdo é o único local permanente para bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Só serão usadas cópias armazenadas em cache se o banco de dados na biblioteca for igual à cópia em disco.  
  
     **Mantenha Banco de dados Inativo em Cache** especifica por quanto tempo um banco de dados inativo permanece no sistema de arquivos depois de ser descarregado da memória. O trabalho de limpeza usa esta configuração para determinar os arquivos a serem excluídos. Todos os bancos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que estiverem inativos por 168 horas (48 horas em memória e 120 horas no cache) serão excluídos do disco pelo trabalho de limpeza.  
  
5.  Clique em **OK** para salvar as alterações.  
  
## <a name="next-steps"></a>Próximas etapas  
 Uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint fornece regras de integridade para que você adote uma ação corretiva ao detectar problemas de integridade do servidor, configuração ou disponibilidade. Algumas dessas regras usam parâmetros de configuração para determinar as condições em que são disparadas regras de integridade. Se você estiver ajustando ativamente o desempenho do servidor, talvez também queira analisar essas configurações para garantir que os padrões sejam a melhor opção para seu sistema. Para obter mais informações, consulte [Configurar regras de integridade do Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-health-rules.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administração e configuração de servidor do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
