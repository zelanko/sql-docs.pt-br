---
title: Configurar o uso de espaço em disco (PowerPivot para SharePoint) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
ms.assetid: 201a3fda-f162-45d7-bf39-74dcb92fd0e6
author: minewiskan
ms.author: owend
manager: craigg
ms.openlocfilehash: fc45827a349dc38054db98e3a435f18a42bdaa0f
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66071806"
---
# <a name="configure-disk-space-usage-powerpivot-for-sharepoint"></a>Configurar o uso do espaço em disco (PowerPivot para SharePoint)
  Uma implantação PowerPivot para SharePoint usa o espaço em disco do computador host para armazenar em cache bancos de dados PowerPivot para agilizar recargas. Todo banco de dados PowerPivot que é carregado em memória primeiro é armazenado em cache em disco para agilizar a recarga posterior para atender novas solicitações. Por padrão, o PowerPivot para SharePoint usa todo o espaço disponível em disco para armazenar em cache seus bancos de dados, mas pode modificar este comportamento definindo propriedades que limitam a quantidade de espaço em disco utilizada.  
  
 Este tópico explica como definir os limites sobre o uso de espaço em disco.  
  
 Este tópico não apresenta orientação para o gerenciamento de espaço em disco de bancos de dados PowerPivot (inseridos em pastas de trabalho do Excel) que são armazenados em bancos de dados de conteúdo. Bancos de dados PowerPivot podem ser grandes, exigindo o aumento da capacidade de memória do farm. Além disso, se o controle de versão estiver habilitado, você poderá perfeitamente ter várias cópias dos dados no mesmo banco de dados de conteúdo, aumentando mais a quantidade de espaço necessário em disco para o armazenamento de conteúdo. Embora bancos de dados PowerPivot sejam uma consideração importante no gerenciamento de disco, eles não podem ser gerenciados independentemente de outro conteúdo armazenado em um farm do SharePoint. Você precisará monitorar ainda mais o espaço em disco à medida que seus negócios fizerem mais uso de pastas de trabalho PowerPivot. Você também pode acompanhar a atividade de pastas de trabalho PowerPivot no Painel de Gerenciamento do PowerPivot e remover pastas de trabalho que não forem mais usadas.  
  
## <a name="how-powerpivot-for-sharepoint-manages-cached-databases"></a>Como o PowerPivot para SharePoint gerencia bancos de dados armazenados em cache  
 Para gerenciar seu cache, o serviço do sistema PowerPivot executa um trabalho em segundo plano em intervalos regulares para limpar bancos de dados não usados ou desatualizados que têm versões mais recentes em uma biblioteca de conteúdo. O propósito do trabalho de limpeza é descarregar bancos de dados inativos da memória e excluir bancos de dados não usados, armazenados em cache do sistema de arquivos. O trabalho de limpeza é para manutenção de longo prazo, garantindo que bancos de dados não permaneçam no sistema por um tempo indefinido. Em um servidor ativo, talvez bancos de dados sejam removidos com mais frequência devido à pressão de memória no servidor, à exclusão de banco de dados no SharePoint ou a versões mais recentes do banco de dados em uma biblioteca de conteúdo.  
  
 Embora você não possa agendar o trabalho de limpeza, pode personalizar o gerenciamento de arquivo de cache definindo propriedades de configuração de servidor que fazem o seguinte:  
  
-   Definir limites na quantidade de espaço em disco usada pelo cache.  
  
-   Especificar o volume de dados a ser excluído quando o espaço máximo em disco é alcançado.  
  
## <a name="how-to-check-disk-space-usage"></a>Como verificar o uso do espaço em disco  
 O PowerPivot para SharePoint é instalado em servidores de aplicativo um farm do SharePoint. Cada instalação tem um diretório de dados que inclui uma pasta Backup. A pasta Backup contém todos os arquivos de dados que são armazenados em cache pela instância do Analysis Services no computador. Por padrão, a pasta Backup pode ser localizada no seguinte caminho:  
  
 `%drive%:\Program Files\Microsoft SQL Server\MSAS10_50.PowerPivot\OLAP\Backup\Sandboxes\<serviceApplicationName>`  
  
 Para verificar o total de espaço em disco usado pelo cache, verifique o tamanho da pasta Backup. Não há propriedades na Administração Central com relatos sobre o tamanho de cache atual.  
  
 A pasta Backup oferece o armazenamento em cache comum para qualquer banco de dados PowerPivot carregado em memória no computador local. Se você tiver vários aplicativos de serviço PowerPivot definidos em seu farm, qualquer um deles poderá usar o servidor local para carregar e subsequentemente armazenar em cache dados PowerPivot. O carregamento e o armazenamento de dados em cache são operações de servidor do Analysis Services. Sendo assim, o uso total de espaço em disco é gerenciado em nível de instância do Analysis Services, na pasta Backup. Parâmetros de configuração que limitam o uso de espaço em disco são definidos na única instância do SQL Server Analysis Services que é executada em um servidor de aplicativos do SharePoint.  
  
 O cache contém apenas bancos de dados PowerPivot. Bancos de dados PowerPivot são armazenados em vários arquivos em uma única pasta pai (a pasta Backup). Como bancos de dados PowerPivot devem ser usados como dados internos em uma pasta de trabalho do Excel, nomes de bancos de dados se baseiam em GUID, e não são descritivos. Uma pasta GUID em  **\<serviceApplicationName >** é a pasta pai de um banco de dados do PowerPivot. Como bancos de dados PowerPivot são carregados no servidor, pastas adicionais são criadas para cada um.  
  
 Como dados PowerPivot podem ser carregados em qualquer instância do Analysis Services em um farm, os mesmos dados também poderiam ser armazenados em cache em vários computadores no farm. Essa prática favorece o desempenho na utilização de espaço em disco, mas a compensação é que os usuários acessam dados mais rápido quando eles já estão disponíveis em disco.  
  
 Para reduzir logo o consumo de espaço em disco, você pode desligar o serviço e, depois, excluir um banco de dados PowerPivot da pasta Backup. A exclusão manual de arquivos é uma medida temporária, pois uma cópia mais nova do banco de dados será armazenada em cache novamente da próxima vez que dados PowerPivot forem consultados. Soluções permanentes incluem a limitação do espaço em disco usado pelo cache.  
  
 Em nível de sistema, você pode criar alertas de email que notifiquem quando o espaço em disco for baixo. O Microsoft System Center inclui um recurso de alerta de email. Você também pode usar o Gerenciador de Recursos do Servidor de Arquivo, o Agendador de Tarefas ou o script PowerShell para configurar alertas. Os links a seguir especificam informações úteis para configurar notificações sobre espaço em disco insuficiente:  
  
-   [O que há de novo no Gerenciador de recursos de servidor de arquivos](https://technet.microsoft.com/library/hh831746.aspx) (https://technet.microsoft.com/library/hh831746.aspx).  
  
-   [Guia passo a passo do Gerenciador de recursos de servidor de arquivos para o Windows Server 2008 R2](https://go.microsoft.com/fwlink/?LinkID=204875) (https://go.microsoft.com/fwlink/?LinkID=204875).  
  
-   [Definindo alertas de espaço em disco insuficiente no Windows Server 2008](https://go.microsoft.com/fwlink/?LinkID=204870) ( https://go.microsoft.com/fwlink/?LinkID=204870).  
  
## <a name="how-to-limit-the-amount-of-disk-space-used-for-storing-cached-files"></a>Como limitar a quantidade de espaço em disco usada para armazenar arquivos em cache  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Serviços no Servidor**.  
  
2.  Clique **SQL Server Analysis Services**.  
  
     Note que os limites são definidos na instância do Analysis Services que é executada no servidor físico, e não em nível de aplicativo de serviço. Todos os aplicativos de serviço que usam a instância do Analysis Services local estão sujeitos ao único limite máximo de espaço em disco que é definido para essa instância.  
  
3.  Em Uso de Disco, defina um valor (em gigabytes) para **Total de espaço em disco** para definir um limite superior na quantidade de espaço usado para fins de cache. O padrão é 0, que permite ao Analysis Services usar todo o espaço disponível em disco.  
  
4.  Uso do disco, nos **excluir armazenados em cache bancos de dados nas últimas ' n'horas** configuração, especifique os critérios usados por último para esvaziar o cache quando o espaço em disco está no limite máximo.  
  
     O padrão são 4 horas, o que significa que todos os bancos de dados que ficaram inativos por 4 horas ou mais serão excluídos do sistema de arquivos. Bancos de dados que estão inativos, mas que permanecem em memória, são descarregados e depois excluídos do sistema de arquivos.  
  
## <a name="how-to-limit-how-long-a-database-is-kept-in-the-cache"></a>Como limitar o tempo de permanência de um banco de dados no cache  
  
1.  Na Administração Central, em Gerenciamento de Aplicativo, clique em **Gerenciar Aplicativos de Serviço**.  
  
2.  Clique em **Aplicativo de Serviço PowerPivot Padrão** para abrir o painel de gerenciamento.  
  
3.  Em Ações, clique em **Definir configurações do aplicativo de serviço**.  
  
4.  Na seção Cache de Disco, você pode especificar quanto tempo um banco de dados permanece inativo em memória para atender novas solicitações (por padrão, 48 horas) e quanto tempo ele permanece no cache (por padrão, 120 horas).  
  
     **Mantenha Banco de dados Inativo em Memória** especifica quanto tempo um banco de dados inativo fica em memória para atender novas solicitações desses dados. Um banco de dados ativo sempre será mantido em memória contanto que você esteja consultando-o, mas depois ele não permanecerá ativo. O sistema manterá o banco de dados em memória por um período de tempo adicional caso existam mais solicitações desses dados.  
  
     Como os bancos de dados PowerPivot primeiro são armazenados em cache e, depois, carregados em memória, os arquivos de banco de dados consomem logo espaço em disco. Entretanto, apesar de o banco de dados estar ativo (e por 48 horas depois disso), todas as solicitações são direcionadas primeiro ao banco de dados em memória, ignorando o banco de dados em cache. Depois de 48 horas de inatividade, o arquivo é descarregado da memória, mas permanece no cache, onde poderá ser recarregado rapidamente se uma nova solicitação de conexão desses dados for interceptada pela instância de servidor do PowerPivot local. As solicitações de conexão a um banco de dados inativo são atendidas do cache e não da biblioteca de conteúdo, minimizando o impacto nos bancos de dados de conteúdo.  
  
     É importante observar que a biblioteca de conteúdo é o único local permanente para bancos de dados PowerPivot. Só serão usadas cópias armazenadas em cache se o banco de dados na biblioteca for igual à cópia em disco.  
  
     **Mantenha Banco de dados Inativo em Cache** especifica por quanto tempo um banco de dados inativo permanece no sistema de arquivos depois de ser descarregado da memória. O trabalho de limpeza usa esta configuração para determinar os arquivos a serem excluídos. Todos os bancos de dados PowerPivot que estiverem inativos por 168 horas (48 horas em memória e 120 horas no cache) serão excluídos do disco pelo trabalho de limpeza.  
  
5.  Clique em **OK** para salvar as alterações.  
  
## <a name="next-steps"></a>Próximas etapas  
 Uma instalação do PowerPivot para SharePoint fornece regras de integridade para que você adote uma ação corretiva ao detectar problemas de integridade do servidor, configuração ou disponibilidade. Algumas dessas regras usam parâmetros de configuração para determinar as condições em que são disparadas regras de integridade. Se você estiver ajustando ativamente o desempenho do servidor, talvez também queira analisar essas configurações para garantir que os padrões sejam a melhor opção para seu sistema. Para obter mais informações, consulte [regras de integridade do PowerPivot - configurar](configure-power-pivot-health-rules.md).  
  
## <a name="see-also"></a>Consulte também  
 [Administração e configuração de servidor do PowerPivot na Administração Central](power-pivot-server-administration-and-configuration-in-central-administration.md)  
  
  
