---
title: Propriedades do servidor (página Avançado) – Reporting Services | Microsoft Docs
ms.custom: ''
ms.date: 2016-10-18
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- reporting-services-native
ms.topic: conceptual
f1_keywords:
- sql12.swb.reportserver.serverproperties.advanced.f1
ms.assetid: 07b78a84-a6aa-4502-861d-349720ef790e
author: markingmyname
ms.author: maghan
manager: craigg
ms.openlocfilehash: 0af66da35bdc42bf78601e3040d91095646a9b75
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48183346"
---
# <a name="server-properties-advanced-page---reporting-services"></a>Propriedades do Servidor (página Avançado) - Reporting Services
  Use essa página para definir propriedades do sistema no servidor de relatórios. Há vários modos de definir propriedades do sistema. Essa ferramenta fornece uma interface gráfica do usuário para que você possa definir propriedades sem precisar gravar código.  
  
 Para abrir essa página, inicie o [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)], conecte-se a uma instância de servidor de relatórios, clique com o botão direito do mouse no nome do servidor de relatórios e selecione **Propriedades**. Clique em **Avançado** para abrir esta página.  
  
## <a name="options"></a>Opções  
 **EnableMyReports**  
 Indica se o recurso Meus Relatórios está habilitado. Um valor de `true` indica que o recurso está habilitado.  
  
 **MyReportsRole**  
 O nome da função usado ao criar políticas de segurança nas pastas de usuário Meus Relatórios. O valor padrão é `My Reports Role`.  
  
 **EnableClientPrinting**  
 Determina se o controle ActiveX de RSClientPrint está disponível para download no servidor de relatório. Os valores válidos são `true` e `false`. O valor padrão é `true`. Para obter mais informações sobre configurações adicionais necessárias para esse controle, consulte [Habilitar e desabilitar a impressão do lado do cliente para Reporting Services](../report-server/enable-and-disable-client-side-printing-for-reporting-services.md).  
  
 **EnableExecutionLogging**  
 Indica se o log de execução de relatório está habilitado. O valor padrão é `true`. Para obter mais informações sobre o log de execução do servidor de relatório, consulte [Log de execução do servidor de relatório e exibição do ExecutionLog3](../report-server/report-server-executionlog-and-the-executionlog3-view.md).  
  
 **ExecutionLogDaysKept**  
 O número de dias para manter informações de execução de relatório no log de execução. Os valores válidos para essa propriedade incluem `-1` por meio `2`,`147`,`483`,`647`. Se o valor for `-1` as entradas não serão excluídas da tabela de log de execução. O valor padrão é `60`.  
  
 **SessionTimeout**  
 A quantidade de tempo, em segundos, que uma sessão permanece ativa. O valor padrão é `600`.  
  
 **SharePointIntegratedMode**  
 Esta é uma propriedade somente leitura que indica o modo do servidor. Se este valor for Falso, o servidor de relatórios executará em modo nativo.  
  
 **SiteName**  
 O nome do site de servidor de relatórios exibido no título da página do Gerenciador de Relatórios. O valor padrão é [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Essa propriedade pode ser uma cadeia de caracteres vazia. O tamanho máximo é de 8.000 caracteres.  
  
 **StoredParametersLifetime**  
 Especifica o número máximo de dias que um parâmetro armazenado pode ser armazenado. Os valores válidos são `-1`, `+1` por meio de `2,147,483,647`. O valor padrão é `180` dias.  
  
 **StoredParametersThreshold**  
 Especifica o número máximo de valores de parâmetro que pode ser armazenado pelo servidor de relatórios. Os valores válidos são `-1`, `+1` por meio de `2,147,483,647`. O valor padrão é `1500`.  
  
 **UseSessionCookies**  
 Indica se o servidor de relatório dever usar cookies de sessão ao se comunicar com navegadores clientes. O valor padrão é `true`.  
  
 **ExternalImagesTimeout**  
 Determina a quantidade de tempo dentro do qual um arquivo de imagem externa deve ser recuperado antes que a conexão expire. O padrão é `600` segundos.  
  
 **SnapshotCompression**  
 Define como os instantâneos são compactados. O valor padrão é `SQL`. Os valores válidos são os seguintes:  
  
 **SQL =** Instantâneos são compactados quando armazenados no banco de dados do servidor de relatórios. Esse é o comportamento atual.  
  
 **None** = Instantâneos não são compactados.  
  
 **All =** Instantâneos são compactados para todas as opções de armazenamento que incluem o banco de dados do servidor de relatórios ou o sistema de arquivos.  
  
 **SystemReportTimeout**  
 O valor do tempo limite de processamento do relatório padrão, em segundos, para todos os relatórios gerenciados no namespace do servidor de relatório. Esse valor pode ser substituído no nível do relatório. Se a propriedade estiver definida, o servidor de relatórios tentará interromper o processamento de um relatório quando o tempo especificado expirar. Os valores válidos são `-1` por meio `2`,`147`,`483`,`647`. Se o valor for `-1`, relatórios no namespace não expirarão durante o processamento. O valor padrão é `1800`.  
  
 **SystemSnapshotLimit**  
 O número máximo de instantâneos que são armazenados para um relatório. Os valores válidos são `-1` por meio `2`,`147`,`483`,`647`. Se o valor for `-1`, não há nenhum limite de instantâneo.  
  
 **EnableIntegratedSecurity**  
 Determina se a segurança integrada do Windows tem suporte para conexões de fonte de dados de relatório. O padrão é `True`. Os valores válidos são os seguintes:  
  
 `True` = a segurança integrada do Windows está habilitada.  
  
 `False` = a segurança integrada do Windows não está habilitada. Fontes de dados de relatório configuradas para usar a segurança integrada do Windows não serão executadas.  
  
 `EnableLoadReportDefinition`  
 Selecione essa opção para especificar se os usuários podem executar relatório ad hoc de um Construtor de Relatórios. Essa opção determina o valor da `EnableLoadReportDefinition` propriedade no servidor de relatório.  
  
 Se você desmarcar esta opção, a propriedade será definida como False e o servidor de relatório não irá gerar relatórios de clickthrough de relatórios que usam um modelo como uma fonte de dados. Qualquer chamada ao método LoadReportDefinition será bloqueada.  
  
 A desativação dessa opção reduz uma ameaça de que um usuário mal-intencionado inicie um ataque de negação de serviço, carregando o servidor de relatórios com solicitações de LoadReportDefinition.  
  
 **EnableRemoteErrors**  
 Inclui informações de erro externo (por exemplo, informações de erros sobre fontes de dados de relatório) com as mensagens de erro retornadas aos usuários que solicitam relatórios de computadores remotos. Os valores válidos são `true` e `false`. O valor padrão é `false`. Para obter mais informações, consulte [Habilitar erros remotos &#40;Reporting Services&#41;](../report-server/enable-remote-errors-reporting-services.md).  
  
 **EnableReportDesignClientDownload**  
 Especifica se o pacote de instalação do Construtor de Relatórios pode ser baixado no servidor de relatórios. Se você desmarcar essa configuração, a URL para o Construtor de Relatórios não funcionará. Para obter mais informações, consulte [Configurar o acesso do Construtor de Relatórios](../report-server/configure-report-builder-access.md).  
  
 **EditSessionCacheLimit**  
 Especifica o número de entradas de cache de dados que podem estar ativas em uma sessão de edição de relatório. O número padrão é 5.  
  
 **EditSessionTimeout**  
 Especifica o número de segundos antes que o tempo limite de uma sessão de edição de relatório seja excedido. O valor padrão é 7200 segundos (2 horas).  
  
 **EnableTestConnectionDetailedErrors**  
 Indica se são enviadas mensagens de erro detalhadas ao computador cliente quando os usuários testam as conexões de fonte de dados usando o servidor de relatório. O valor padrão é `true`. Se a opção é definida como `false`, apenas as mensagens de erro genéricas são enviadas.  
  
## <a name="see-also"></a>Consulte também  
 [Definir propriedades do servidor de relatório &#40;Management Studio&#41;](set-report-server-properties-management-studio.md)   
 [Conectar-se a um servidor de relatório no Management Studio](connect-to-a-report-server-in-management-studio.md)   
 [Propriedades do Reporting Services](../report-server-web-service/net-framework/reporting-services-properties.md)   
 [Servidor de Relatório na ajuda F1 do Management Studio](report-server-in-management-studio-f1-help.md)   
 [Propriedades do sistema do servidor de relatório](../report-server-web-service/net-framework/reporting-services-properties-report-server-system-properties.md)   
 [Implantação de script e tarefas administrativas](script-deployment-and-administrative-tasks.md)   
 [Habilitar e desabilitar Meus Relatórios](../report-server/enable-and-disable-my-reports.md)  
  
  
