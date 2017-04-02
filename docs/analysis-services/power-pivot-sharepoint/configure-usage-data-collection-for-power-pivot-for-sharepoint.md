---
title: "Configurar a coleta de dados de uso para o Power Pivot para SharePoint | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "analysis-services"
  - "analysis-services/multidimensional-tabular"
  - "analysis-services/data-mining"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: 955ca6d6-9d5b-47a4-a87c-59bd23f1bf74
caps.latest.revision: 10
author: "Minewiskan"
ms.author: "owend"
manager: "erikre"
caps.handback.revision: 9
---
# Configurar a coleta de dados de uso para o Power Pivot para SharePoint
  A coleta de dados de uso é um recurso do SharePoint em nível de farm. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint usa e estende esse sistema para fornecer relatórios no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que mostram como os dados e serviços do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são usados. Dependendo da forma como você instala o SharePoint, a coleta de dados de uso poderá ser desativada para o farm. Um administrador de farm deve habilitar o registro em log de uso para criar os dados de uso exibidos no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
 Para obter informações sobre os dados de uso no Painel de Gerenciamento [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], consulte [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
 **Neste tópico:**  
  
 [Habilite a coleta de dados de uso e escolha eventos que disparem a coleta de dados](#events)  
  
 [Definir local do arquivo de log](#configdb)  
  
 [Configure os trabalhos de timer usados em coleta de dados de uso](#jobs)  
  
 [Limite o tempo de armazenamento do histórico de dados de uso](#confighist)  
  
 [Defina categorias de resposta de consulta rápida, média e lenta para fins de relatórios](#qrh)  
  
 [Especifique a frequência dos relatórios estatísticas de consulta para o sistema de coleta de dados de uso](#ttr)  
  
 [Abra a página Aplicativo do Serviço Power Pivot para acessar as definições de configuração](#openconfig)  
  
 [A configuração padrão da coleta de dados de uso do Power Pivot](#defaultconfig)  
  
> [!IMPORTANT]  
>  Dados de uso fornecem aprofundamento sobre como os usuários estão acessando dados e recursos, mas eles não garantem dados confiáveis, persistentes sobre operações de servidor e acesso de usuário. Por exemplo, se houver uma reinicialização de servidor, dados de uso de evento serão perdidos e não serão recuperáveis. Da mesma forma, se os arquivos de log temporários atingirem o tamanho máximo, nenhum novo dado será adicionado até que os arquivos sejam desmarcados. Se você precisa do recurso de auditoria, procure usar os recursos de fluxo de trabalho e tipo de conteúdo que o SharePoint fornece para criar um subsistema de auditoria para seu farm. Para obter mais informações, consulte a documentação do produto e da comunidade na Web.  
  
##  <a name="events"></a> Habilite a coleta de dados de uso e escolha eventos que disparem a coleta de dados  
 Configure a coleta de dados de uso na Administração Central do SharePoint.  
  
1.  Na Administração Central, clique em **Monitoramento**.  
  
2.  Na seção **Relatórios**, clique em **Configurar coleta de dados de integridade e uso**.  
  
3.  Selecione a opção **Habilitar coleta de dados de uso**.  
  
4.  Na seção **Eventos para o log** , marque ou desmarque as caixas de seleção para habilitar ou desabilitar os seguintes eventos do Analysis Services:  
  
    |Evento|Description|  
    |-----------|-----------------|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Conexões**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é usado para monitorar conexões de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que são feitas em nome de um usuário.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Uso de Dados de Carregamento**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é usado para monitorar solicitações que carregam dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] na memória do servidor. Um evento de carregamento é gerado para arquivos de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] carregadas de um banco de dados de conteúdo ou de cache.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Uso de Dados de Descarregamento**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é usado para monitorar solicitações de descarregamento de uma fonte de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] após um período de inatividade. O armazenamento em cache de uma fonte de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no disco será relatado como um evento de descarregamento.|  
    |**[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Uso de Consulta**|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é usado para monitorar os tempos de processamento dos dados carregados em uma instância do [!INCLUDE[ssGeminiSrv](../../includes/ssgeminisrv-md.md)] .|  
  
    > [!NOTE]  
    >  As operações de integridade do servidor e atualização de dados também geram dados de uso, mas não há evento associado com esses processos.  
  
5.  Você também pode atualizar o local do arquivo de log. Para obter mais informações, consulte a próxima seção.  
  
6.  Clique em **OK** para salvar as alterações.  
  
7.  Opcionalmente, você pode especificar se todas as mensagens ou apenas erros são registrados em log. Para obter mais informações sobre como acelerar as mensagens de evento, consulte [Configurar e exibir arquivos de log do SharePoint e log de diagnóstico e 40;Power Pivot para SharePoint&41;](../Topic/Configure%20and%20View%20SharePoint%20Log%20Files%20%20and%20Diagnostic%20Logging%20\(Power%20Pivot%20for%20SharePoint\).md).  
  
##  <a name="configdb"></a> Definir local do arquivo de log  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são armazenados inicialmente em arquivos de log de uso no servidor local e movidos em intervalos regulares para os bancos de dados de aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O local do arquivo de log é definido na Administração Central. O local padrão é:  
  
 `C:\Program Files\Common Files\Microsoft Shared\Web Server Extensions\15\logs`  
  
 Para exibir ou alterar essas propriedades, use a página **Coleta de dados de uso e integridade** .  
  
1.  Na página inicial da Administração Central, clique em **Monitoramento**.  
  
2.  Na seção Monitoramento, clique em **Confirmar uso e coleta de dados de integridade**.  
  
3.  Em Configurações de Coleta de Dados de Uso, exiba ou modifique a localização do arquivo, o nome ou o tamanho máximo do arquivo. Se você especificar um tamanho de arquivo muito baixo, o tamanho de arquivo alcançará o limite máximo e nenhuma nova entrada será adicionada a ele até que seu conteúdo seja movido para o banco de dados de coleta de dados de uso central.  
  
##  <a name="jobs"></a> Configure os trabalhos de timer usados em coleta de dados de uso  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são movidos para locais diferentes no sistema de coleta de dados de uso por dois trabalhos do temporizador:  
  
-   O trabalho do temporizador “Importação de Dados de Uso do Microsoft SharePoint Foundation” move o uso do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para o banco de dados de aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
-   O trabalho do temporizador “Processamento de Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]” move os dados para a pasta de trabalho do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)], que é a fonte de dados dos relatórios administrativos internos.  
  
 Se você precisar atualizar os relatórios administrativos que aparecem com maior frequência no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , siga estas etapas.  
  
1.  Na Administração Central, clique em **Monitoramento**.  
  
2.  Clique em **Revisar definições de trabalho** Na seção **Trabalhos de timer** .  
  
3.  Clique em **Importação de Dados de Uso do Microsoft SharePoint Foundation**.  
  
4.  Clique em **Executar Agora**. Se o botão **Executar Agora** for desabilitado, clique em **Habilitar** e clique em **Executar Agora**.  
  
5.  Na lista Definições de Trabalho, clique em **Trabalho do Temporizador do Processamento do Painel de Gerenciamento de Dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]**.  
  
6.  Clique em **Executar Agora**.  
  
7.  Verifique os relatórios para exibir os dados de atualização. Para obter mais informações, consulte [Power Pivot Management Dashboard and Usage Data](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md).  
  
##  <a name="confighist"></a> Limite o tempo de armazenamento do histórico de dados de uso  
 O histórico de dados de uso é armazenado para eventos (conexões, carga, descarga e processamento de consulta sob demanda) e atualização de dados (processamento de dados agendado). Embora dados de uso sejam coletados pelo sistema de coleta de dados de uso do SharePoint, os dados de relatório são movidos para um banco de dados de aplicativo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e para um banco de dados de relatório para armazenamento por um prazo maior. A definição do histórico de dados de uso controla por quanto tempo dados de uso são retidos nos bancos de dados de aplicativo [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O mesmo limite se aplica igualmente a todos os tipos de dados de uso armazenados no mesmo banco de dados do aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .  
  
1.  [Abra a página do aplicativo de serviço Power Pivot](#openconfig).  
  
2.  Na seção **Coleta de Dados de Uso** , em **Histórico de Dados de Uso**, digite o número de dias dos quais você deseja manter um registro da atividade de atualização de dados de cada pasta de trabalho.  
  
    -   O padrão é 365 dias.  
  
    -   0 especifica armazenamento ilimitado onde dados de uso são mantidos indefinidamente.  
  
    -   Outra alternativa é especificar um intervalo entre 1 e 5000.  
  
     A redução do período de retenção para um número menor de dias excluirá dados que excedam o novo limite. Por exemplo, a alteração do valor de 365 para 30 resultará na exclusão de dados de uso para obter todas as informações históricas que ocorreram mais de 30 dias atrás. Apenas dados dos últimos 30 dias são retidos.  
  
     Dados são excluídos de fato quando o próximo evento ocorre. O limite no histórico de dados de uso só é verificado quando o sistema processa um evento.  
  
3.  Clique em **OK**.  
  
 Para obter mais informações sobre como os dados de uso são coletados e armazenados, consulte [Coleta de dados de uso do Power Pivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).  
  
##  <a name="qrh"></a> Defina categorias de resposta de consulta rápida, média e lenta para fins de relatórios  
 O desempenho de processamento da consulta é medido em relação a categorias predefinidas que definem um ciclo da solicitação-resposta pelo tempo que leva para ser concluído. Categorias predefinidas incluem: Trivial, Rápido, Esperado, Demorado e Excedido. Toda solicitação para um servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] corresponderá a uma das categorias com base no tempo para conclusão.  
  
 As informações de resposta da consulta são usadas em relatórios de atividades. Dentro dos relatórios, cada categoria é usada diferentemente para revelar melhor as tendências de desempenho do sistema [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por exemplo, são totalmente excluídas solicitações triviais pois isso remove ruídos nos dados e mostra tendências mais significativas que usam as categorias restantes. Em contraste, estatísticas de solicitação Demorado ou Excedido são proeminentes no relatório de forma que administradores ou proprietários de pasta de trabalho podem adotar uma ação corretiva imediatamente.  
  
 Embora você não possa adicionar ou excluir categorias, pode definir os limites superiores e inferiores que determinam onde uma categoria é interrompida e a próxima começa. Se sua organização usar SLA (Acordos em Nível de Serviço) para definir níveis aceitáveis de disponibilidade e desempenho do servidor, você poderá ajustar essas categorias para refletir o SLA criado.  
  
1.  [Abra a página do aplicativo de serviço Power Pivot](#openconfig).  
  
2.  Na seção **Coleta de Dados de Uso**, em **Limite Superior de Resposta Trivial**, digite um valor (em milissegundos) que defina o limite superior para a conclusão de uma resposta trivial. Solicitações que costumam se encaixar nessa categoria incluem pings de servidor, iniciação de sessão e consulta de metadados. O padrão é 500 milissegundos (ou meio segundo).  
  
3.  Em Limite Superior de Solicitações Rápidas, insira um valor (em milissegundos) que define o limite superior para concluir uma resposta rápida. Solicitações que se encaixam nesta categoria incluem consultas de conjuntos de dados muito pequenos ou servidores de metadados de conjuntos de dados grandes. O padrão é 1000 milissegundos (ou 1 segundo).  
  
4.  Em **Limite Superior de Resposta Esperado**, digite um valor (em milissegundos) que defina o limite superior para a conclusão de uma resposta em um período de tempo esperado ou médio. Solicitações que entram nesta categoria incluem o carregamento de dados em um visualizador. O padrão é 3000 milissegundos (ou 3 segundos).  
  
5.  Em **Limite Superior de Resposta Lenta**, digite um valor (em milissegundos) que defina o limite superior para a conclusão de uma resposta demorada. Solicitações que entram nesta categoria demoram mais do que o esperado, mas dentro de um intervalo ainda aceitável. O padrão é 10000 milissegundos (ou 10 segundos).  
  
     Qualquer solicitação que exceda esse limite será categorizado como *Excedida*. Não há limite configurável para *Excedida*. Isso é inferido a partir do limite superior que você especifica em Limite Superior de Solicitações Longas. Solicitações que entram na categoria Excedido são executadas por mais muito tempo do que é permitido por um SLA que você definiu.  
  
6.  Clique em **OK**.  
  
##  <a name="ttr"></a> Especifique a frequência dos relatórios estatísticas de consulta para o sistema de coleta de dados de uso  
 O intervalo de tempo para relatório especifica a frequência dos relatórios estatísticas de consulta para o sistema de coleta de dados de uso. Estatísticas de consulta são acumuladas em um processo e relatadas como um único evento em intervalos regulares. Você pode ajustar o intervalo para gravar no arquivo de log com maior ou menor frequência.  
  
1.  [Abra a página do aplicativo de serviço Power Pivot](#openconfig).  
  
2.  Na seção **Coleta de Dados de Uso**, em **Intervalo de Relatório de Consulta**, digite o número de segundos depois dos quais o servidor relatará as estatísticas de consulta para todas as categorias (trivial, rápido, esperado, demorado e excedido) como um único evento para o sistema de coleta de dados de uso.  
  
    -   O intervalo é 1 para qualquer inteiro positivo.  
  
    -   O padrão é 300 segundos (ou 5 minutos). Este valor é recomendado para ambientes de farm dinâmicos que executam uma variedade de aplicativos e serviços.  
  
     Se você aumentar este valor para um número muito maior, poderá perder dados estatísticos antes de eles serem relatados. Por exemplo, uma reinicialização de serviço causará a perda de estatísticas de consulta. Por outro lado, se seus relatórios de atividades internas mostram dados insuficientes, procure diminuir o intervalo para obter eventos tempo-para-relatório com maior frequência.  
  
3.  Clique em **OK**.  
  
##  <a name="openconfig"></a> Abra a página Aplicativo do Serviço Power Pivot para acessar as definições de configuração  
 Você deve ser um administrador de farm ou de serviço para modificar as configurações do aplicativo de serviço. Se você definiu vários aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] no farm, deverá modificar cada um deles individualmente.  
  
1.  Na Administração Central do SharePoint, em **Gerenciamento de Aplicativo**, clique em **Gerenciar aplicativos de serviço**.  
  
2.  Encontre o aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Você pode identificar um aplicativo de serviço por seu tipo. Um tipo de aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é **[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Aplicativo de Serviço**.  
  
3.  Clique no nome do aplicativo de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . O Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é aberto.  
  
4.  Em **Ações**, clique em **Configurar parâmetros do aplicativo de serviço**. A página Configurações do Aplicativo do Serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] será aberta.  
  
##  <a name="defaultconfig"></a> A configuração padrão da coleta de dados de uso do Power Pivot  
 Operações de coleta de dados de uso para serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] podem ser habilitadas com configurações padrão disponibilizá-las imediatamente em aplicativos que dão suporte ao recurso de integração Analysis Services. As configurações padrão incluem eventos que disparam coleta de dados de uso, limites sobre o tempo de armazenamento de dados de uso, e limites para categorizar tempos de resposta de consulta.  
  
 A tabela a seguir mostra os valores padrão da configuração da coleta de dados de uso.  
  
|Configuração|Valor padrão|Tipo|Intervalo válido|  
|-------------|-------------------|----------|-----------------|  
|**Eventos de uso do Analysis Services** (Conexão, Carregamento, Descarregamento, Solicitações)|\<enabled>|Booliano|Estes valores são habilitados ou desabilitados.|  
|**Intervalo de relatório de consulta**|300 (em segundos)|Integer|1 até qualquer inteiro positivo. O padrão é 5 minutos.|  
|**Histórico de dados de uso**|365 (em dias)|Integer|0 especifica ilimitado, mas você também pode definir um limite superior para expirar dados históricos e permitir sua exclusão automática. Valores válidos para um período de retenção limitado variam de 1 a 5000 (em dias).|  
|Limite superior de resposta trivial|500 (em milissegundos)|Integer|Define um limite superior que define uma troca de solicitação-resposta trivial. Qualquer solicitação concluída entre 0 e 500 milissegundos é uma solicitação trivial e ignorada para fins de relatórios.|  
|Limite superior de resposta rápida|1000 (em milissegundos)|Integer|Define um limite superior que define uma troca de solicitação-resposta rápida.|  
|Limite superior de resposta esperada|3000 (em milissegundos)|Integer|Define um limite superior que define uma troca de solicitação-resposta esperada.|  
|Limite Superior de Respostas Demoradas|10000 (em milissegundos)|Integer|Define um limite superior que define uma troca de solicitação-resposta demorada. Qualquer solicitação que exceda esse limite superior entrará na categoria Excedida, que não tem limite superior.|  
  
## Consulte também  
 [Referência de parâmetro de configuração &#40;Power Pivot para SharePoint&#41;](../../analysis-services/power-pivot-sharepoint/configuration-setting-reference-power-pivot-for-sharepoint.md)   
 [Coleta de dados de uso do PowerPivot](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md)  
  
  