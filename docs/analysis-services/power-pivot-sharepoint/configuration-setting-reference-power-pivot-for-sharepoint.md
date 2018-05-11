---
title: Configuração de referência (PowerPivot para SharePoint) | Microsoft Docs
ms.date: 05/02/2018
ms.prod: sql
ms.technology: analysis-services
ms.component: ppvt-sharepoint
ms.topic: conceptual
ms.author: owend
ms.reviewer: owend
author: minewiskan
manager: kfile
ms.openlocfilehash: d58ca9b3c3769a34164157f7297269f100ea8c1d
ms.sourcegitcommit: 38f8824abb6760a9dc6953f10a6c91f97fa48432
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/10/2018
---
# <a name="configuration-setting-reference-power-pivot-for-sharepoint"></a>Referência de parâmetro de configuração (Power Pivot para SharePoint)
[!INCLUDE[ssas-appliesto-sqlas](../../includes/ssas-appliesto-sqlas.md)]
  Este tópico fornece documentação de referência para os parâmetros de configuração usados por aplicativos de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] em um farm do SharePoint. Se você estiver usando script do PowerShell para configurar um servidor ou se desejar procurar informações para uma configuração específica, as informações deste tópico fornecerão descrições detalhadas.  
  
 Os parâmetros de configuração são definidos para cada aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Em um farm, você pode criar diversos aplicativos de serviço como uma maneira de configurar instâncias lógicas independentes da mesma instância física de serviço. Os parâmetros de configuração são armazenados no banco de dados de aplicativo do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] criado para cada aplicativo de serviço configurado.  
  
 Se você alterar os parâmetros de configuração, as alterações serão selecionadas imediatamente e usadas para solicitações e conexões subsequentes. Operações que estão em andamento são governadas pelas configurações que estavam em vigor no início da operação.  
  
 Clique nos links a seguir para ler sobre áreas de configuração específicas:  
  
 [Tempo limite de carregamento de dados](#LoadingData)  
  
 [Pools de conexões](#ConnectionPool)  
  
 [Balanceamento de carga](#AllocationScheme)  
  
 [Atualização de Dados](#DataRefresh)  
  
 [Coleta de dados de uso](#UsageData)  
  
 Para obter instruções sobre como criar um aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , consulte [Criar e configurar um aplicativo de serviço do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md).  
  
##  <a name="LoadingData"></a> Tempo limite de carregamento de dados  
 [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] são recuperados e carregados pelas instâncias de servidor do Analysis Services no farm. Dependendo de como e quando os dados foram acessados pela última vez, eles serão carregados de uma biblioteca de conteúdo ou de um cache de arquivo local. Os dados são carregados na memória sempre que uma solicitação de consulta ou processamento é recebida. Para maximizar a disponibilidade geral do servidor, você pode definir um valor de tempo limite que instrua o servidor a parar uma solicitação de dados de carregamento se ela não puder ser concluída dentro do tempo alocado.  
  
|Nome|Padrão|Valores válidos|Description|  
|----------|-------------|------------------|-----------------|  
|Tempo limite de carregamento de dados|1.800 (em segundos)|1 a 3.600|Especifica a quantidade de tempo que um aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] esperará por uma resposta de uma instância específica do servidor do Analysis Services.<br /><br /> Por padrão, o aplicativo de serviço espera 30 minutos por uma carga de dados da instância de serviço de mecanismo para a qual foi encaminhada uma solicitação específica.<br /><br /> Se a fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não puder ser carregada dentro desse período de tempo, o thread será interrompido e um novo será iniciado.|  
  
##  <a name="ConnectionPool"></a> Pools de conexões  
 O aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] cria e gerencia pools de conexões para habilitar a reutilização da conexão. Há dois tipos de pools de conexões: um para conexões de dados somente leitura e um segundo para conexões de servidor.  
  
 Os pools de conexões de dados contêm conexões armazenadas em cache para a fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Cada pool de conexão é baseado no contexto definido quando o banco de dados foi carregado. Esse contexto inclui a identidade da instância física de serviço, a ID do banco de dados e a identidade do usuário do SharePoint que está solicitando os dados. Um pool de conexão separado é criado para cada combinação. Por exemplo, solicitações de usuários diferentes do mesmo banco de dados em execução no mesmo servidor consumirão conexões de pools diferentes.  
  
 A finalidade de um pool de conexão é usar conexões armazenadas em cache para solicitações somente leitura para o mesmo banco de dados do Analysis Services pelo mesmo usuário do SharePoint. A instância de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] é o servidor que tem os dados carregados na memória. A ID do banco de dados é um identificador interno para as estruturas de dados na memória do modelo de dados (a instância de um modelo é criada como um banco de dados de cubos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] ). As informações de versão são incorporadas implicitamente no identificador.  
  
 Os pools de conexões de servidor contêm conexões armazenadas em cache de uma instância de aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para uma instância de servidor do Analysis Services, no qual o aplicativo de serviço está conectando com permissões de Sysadmin do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] no servidor do Analysis Services. Essas conexões são usadas para emitir uma solicitação de banco de dados de carregamento e para monitorar a integridade do sistema.  
  
 Cada tipo de pool de conexão tem limites superiores que podem ser definidos para garantir um melhor uso da memória do sistema para o gerenciamento de conexões.  
  
|Nome|Padrão|Valores válidos|Description|  
|----------|-------------|------------------|-----------------|  
|Tempo limite do pool de conexões|1.800 (em segundos)|1 a 3.600.|Essa configuração se aplica a pools de conexão de dados.<br /><br /> Especifica por quanto tempo uma conexão ociosa pode permanecer em um pool de conexão antes de ser removida.<br /><br /> Por padrão, o aplicativo de serviço removerá uma conexão se ela estiver inativa por mais de cinco minutos.|  
|Tamanho máximo do pool de conexões de usuário|1.000|-1, 0, ou 1 a 10000.<br /><br /> -1 especifica um número ilimitado de conexões ociosas.<br /><br /> 0 indica que nenhuma conexão ociosa é mantida. Novas conexões com uma fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] devem ser criadas de cada vez.|Essa configuração se aplica ao número de conexões ociosas em todos os pools de conexão de dados criados para uma instância do aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] específica.<br /><br /> Pools de conexão individuais são criados para combinações exclusivas de um usuário do SharePoint, dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] e instância de serviço. Se você tiver muitos usuários acessando uma variedade de fontes de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , o desempenho do servidor poderá se beneficiar com um aumento no tamanho do pool de conexão.<br /><br /> Se houver mais de 100 conexões ociosas a uma instância de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , novas conexões ociosas serão desconectadas em vez de serem retornadas ao pool.|  
|Tamanho máximo do pool de conexões administrativas|200|-1, 0, ou 1 a 10000.<br /><br /> -1 especifica um número ilimitado de conexões ociosas.|O número máximo de conexões de servidor ociosas em todos os pools de conexão administrativos criados para conexões de aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] a uma instância de servidor do Analysis Services. As conexões de servidor são usadas para solicitações para carregar bancos de dados e para salvar alterações no banco de dados do SharePoint.|  
  
##  <a name="AllocationScheme"></a> Balanceamento de carga  
 Uma das funções que o serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] executa é determinar onde os dados do Analysis Services serão carregados entre as instâncias de serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] disponíveis. A configuração **AllocationMethod** especifica os critérios em relação aos quais uma instância de serviço é selecionada.  
  
|Nome|Padrão|Valores válidos|Description|  
|----------|-------------|------------------|-----------------|  
|Método de alocação|RoundRobin|Round Robin<br /><br /> Baseado na Integridade|Um esquema para alocar solicitações de carga entre duas ou mais instâncias de servidor do Analysis Services.<br /><br /> Por padrão, o serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] alternará solicitações com base na integridade do servidor. A opção Baseado na Integridade aloca solicitações ao servidor que tem a maioria dos recursos do sistema disponíveis com base na memória disponível e na utilização da CPU.<br /><br /> Rodízio gira solicitações entre os servidores disponíveis em ordem sequencial, independentemente da carga atual ou da integridade do servidor.|  
  
##  <a name="DataRefresh"></a> Atualização de Dados  
 Especifique o intervalo de horas que define um dia comercial normal ou típico de sua organização. Esses parâmetros de configuração determinam quando, depois do horário comercial, ocorre o processamento das operações de atualização de dados. O processamento depois do horário comercial pode começar no final do dia comercial. O processamento depois do horário comercial é uma opção de agenda para proprietários de documentos que desejam atualizar uma fonte de dados [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] com dados transacionais gerados durante o horário comercial normal.  
  
|Nome|Padrão|Valores válidos|Description|  
|----------|-------------|------------------|-----------------|  
|Hora de início|4h00|1 a 12 horas, quando o valor for um inteiro válido dentro desse intervalo.<br /><br /> O tipo é Time.|Define o limite inferior de um intervalo de horário comercial.|  
|Hora de término|20h00|1 a 12 horas, quando o valor for um inteiro válido dentro desse intervalo.<br /><br /> O tipo é Time.|Define o limite superior de um intervalo de horário comercial.|  
|[!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] Conta autônoma de atualização de dados|Nenhuma|A ID de um aplicativo de destino|Esta conta é usada para executar trabalhos de atualização de dados em nome de um proprietário de agenda.<br /><br /> A conta autônoma de atualização de dados deve ser definida com antecedência antes de poder ser referenciada na página de configuração do aplicativo de serviço. Para obter mais informações, consulte [Configurar a conta autônoma da atualização de dados do Power Pivot (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/81401eac-c619-4fad-ad3e-599e7a6f8493).|  
|Permitir que usuários digitem credenciais do Windows personalizadas|Ativado|Booliano|Determina se a página de configuração de atualização de dados agendada mostra uma opção que permite que um proprietário de agenda especifique conta de usuário do Windows e senha para executar um trabalho de atualização de dados.<br /><br /> O Serviço de Repositório Seguro deve ser habilitado para que esta opção funcione. Para obter mais informações, consulte [Configurar credenciais armazenadas para atualização de dados do Power Pivot (Power Pivot para SharePoint)](http://msdn.microsoft.com/en-us/987eff0f-bcfe-4bbd-81e0-9aca993a2a75).|  
|Comprimento máximo de histórico de processamento|365|1 a 5000 dias|Determina por quanto tempo o histórico de dados será retido no banco de dados de aplicativo de serviço do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Para obter mais informações, consulte [Power Pivot Usage Data Collection](../../analysis-services/power-pivot-sharepoint/power-pivot-usage-data-collection.md).|  
  
##  <a name="UsageData"></a> Coleta de dados de uso  
 Os relatórios de uso que aparecem no Painel de Gerenciamento do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] podem fornecer informações importantes sobre como as pastas de trabalho habilitadas para o [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]são usadas. Os parâmetros de configuração a seguir controlam aspectos da coleta de dados de uso para eventos de servidor do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] que são apresentados subsequentemente em relatórios de uso ou de atividades.  
  
|Nome|Padrão|Valores válidos|Description|  
|----------|-------------|------------------|-----------------|  
|Intervalo de relatório de consulta.|300 (em segundos)|1 a n segundos, onde n é qualquer inteiro válido.|Para garantir que a coleta de dados de uso não consuma muito da capacidade de transferência de dados do farm, estatísticas de consulta são coletadas em cada conexão e relatadas como um único evento. O Intervalo de relatório de consulta determina com que frequência é relatado um evento. Por padrão, as estatísticas de consulta são relatadas a cada 5 minutos.<br /><br /> Como as conexões são fechadas imediatamente assim que uma solicitação é enviada, o sistema gera um número muito grande de conexões para até mesmo um único usuário que acessa uma única fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Por isso, são criados pools de conexão para cada usuário e combinação de fonte de dados do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] , de forma que depois que uma conexão é criada, ela pode ser reutilizada pelo mesmo usuário para os mesmos dados. Periodicamente, em intervalos especificados por esse parâmetro de configuração, o aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] relata os dados de uso de cada conexão no pool de conexão.<br /><br /> O aumento do valor do tempo de relatório fará com que menos eventos sejam registrados em log. No entanto, se um valor muito alto for definido, você arriscará perder dados de eventos se o servidor for reiniciado ou se uma conexão for fechada.<br /><br /> A redução do valor fará com que mais eventos sejam registrados em log com maior frequência, adicionando mais dados de uso relacionados ao [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)]ao sistema de coleta de dados no banco de dados de uso do SharePoint.<br /><br /> De modo geral, não altere esse parâmetro de configuração a menos que você esteja tentando resolver um problema específico (por exemplo, se o banco de dados de uso estiver crescendo muito rapidamente como resultado dos dados de uso do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] ).|  
|Histórico de dados de uso|365 (em dias)|0 ou 1 a n dias, onde n é qualquer inteiro válido.<br /><br /> 0 significa que o histórico sempre é retido e que nunca é excluído.|Por padrão, os dados de uso são mantidos durante um ano no banco de dados do aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] . Registros mais antigos do que um ano são removidos do banco de dados.<br /><br /> Uma verificação dos dados históricos expirados ocorre diariamente quando o trabalho de processamento de dados de uso do Microsoft SharePoint Foundation é executado. O trabalho do temporizador lerá essa configuração e disparará um comando de exclusão dos dados do histórico expirado do banco de dados do aplicativo do serviço [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] .|  
|Limite superior de resposta trivial|500 (em milissegundos)|1 a n milissegundos, onde n é qualquer inteiro válido.|Por padrão, o limite para solicitações triviais é de meio segundo.<br /><br /> As solicitações triviais incluem pings no servidor, solicitações de metadados e início de sessões.|  
|Limite superior de resposta rápida|1000 (em milissegundos)|1 a n milissegundos, onde n é qualquer inteiro válido.|Por padrão, o limite para solicitações rápidas é de um segundo.<br /><br /> As solicitações rápidas são as que têm um conjunto de dados extremamente pequeno ou solicitações de metadados que se estendem por grandes conjuntos de membros.|  
|Limite Superior de Resposta Esperado|3000 (em milissegundos)|1 a n milissegundos, onde n é qualquer inteiro válido.|Por padrão, o limite para solicitações esperadas é de três segundos.<br /><br /> Esse limite define o limite superior de um tempo de consulta esperada.|  
|Limite superior de resposta longa|10000 (em milissegundos)|1 a n milissegundos, onde n é qualquer inteiro válido.|Por padrão, o limite para solicitações longas é de dez segundos.<br /><br /> Essas são solicitações que executam por muito mais tempo do que o esperado, mas que ainda caem dentro de um intervalo aceitável.|  
  
## <a name="see-also"></a>Consulte também  
 [Criar e configurar um aplicativo de serviço do Power Pivot na Administração Central](../../analysis-services/power-pivot-sharepoint/create-and-configure-power-pivot-service-application-in-ca.md)   
 [Atualização de dados do Power Pivot com o SharePoint 2010](http://msdn.microsoft.com/en-us/01b54e6f-66e5-485c-acaa-3f9aa53119c9)   
 [Configurar a coleta de dados de uso para o &#40;Power Pivot para SharePoint](../../analysis-services/power-pivot-sharepoint/configure-usage-data-collection-for-power-pivot-for-sharepoint.md)   
 [Configurar contas de serviço Power Pivot](../../analysis-services/power-pivot-sharepoint/configure-power-pivot-service-accounts.md)   
 [Painel de Gerenciamento Power Pivot e dados de uso](../../analysis-services/power-pivot-sharepoint/power-pivot-management-dashboard-and-usage-data.md)  
  
  
