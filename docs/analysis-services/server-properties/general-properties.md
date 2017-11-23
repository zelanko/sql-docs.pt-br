---
title: Propriedades gerais | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: analysis-services
ms.service: 
ms.component: server-properties
ms.reviewer: 
ms.suite: sql
ms.technology: analysis-services
ms.tgt_pltfrm: 
ms.topic: reference
helpviewer_keywords:
- IdleConnectionTimeout property
- InstanceVisible property
- TempDir property
- AdminTimeout property
- MinIdleSessionTimeout property
- MaxIdleSessionTimeout property
- IdleOrphanSessionTimeout property
- BackupDir property
- CommitTimeout property
- ExternalCommandTimeout property
- Enabled property
- ForceCommitTimeout property
- Port property
- CoordinatorShutdownMode property
- ServerTimeout property
- AllowedBrowsingFolders property
- CoordinatorCancelCount property
- DataDir property
- CoordinatorQueryMaxThreads property
- CoordinatorExecutionMode property
- ExternalConnectionTimeout property
- CollationName property
- EnableFast1033Locale property
- CoordinatorBuildMaxThreads property
- Language property
- StatisticsStoreSize property
- RepositoryConnectionString property
ms.assetid: 88a8117c-396a-469f-a62d-c6f262504021
caps.latest.revision: "31"
author: Minewiskan
ms.author: owend
manager: kfile
ms.workload: Inactive
ms.openlocfilehash: f855fdbc56dee39c971448dd5e764c5490fb176e
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="general-properties"></a>Propriedades gerais
  [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] oferece suporte às propriedades do servidor listadas nas tabelas a seguir. Este tópico documenta essas propriedades de servidor no arquivo msmdsrv.ini que não são incluídas em uma seção específica, como Segurança, Rede ou ThreadPool. Para obter mais informações sobre propriedades adicionais do servidor e como defini-las, consulte [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md).  
  
 **Aplica-se a:** modo de servidor Multidimensional e de Tabela, a menos que indicado em contrário  
  
## <a name="non-specific-category"></a>Categoria não específica  
 **AdminTimeout**  
 Uma propriedade de inteiro de 32 bits assinada que define o tempo limite do administrador em segundos. Essa é uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 O valor padrão dessa propriedade é zero (0), que indica que não há tempo limite.  
  
 **AllowedBrowsingFolders**  
 Uma propriedade de cadeia de caracteres que especifica em uma lista delimitada as pastas que podem ser procuradas ao salvar, abrir e localizar arquivos em caixas de diálogo do Analysis Services. A conta de serviço do Analysis Services deve ter permissões de leitura e gravação em qualquer pasta adicionada à lista.  
  
 **BackupDir**  
 Uma propriedade de cadeia de caracteres que identifica o nome do diretório em que os arquivos de backup estão armazenados por padrão, para a eventualidade de o caminho não ser especificado como parte do comando Backup.  
  
 **CollationName**  
 Uma propriedade de cadeia de caracteres que identifica o agrupamento do servidor. Para obter mais informações, consulte [Idiomas e agrupamentos &#40;Analysis Services&#41;](../../analysis-services/languages-and-collations-analysis-services.md).  
  
 **CommitTimeout**  
 Uma propriedade integer que especifica quanto tempo (em milissegundos) o servidor aguardará para adquirir um bloqueio de gravação visando confirmar uma transação. Um período de espera costuma ser necessário porque o servidor precisa aguardar que outros bloqueios sejam liberados para usar um bloqueio de gravação que confirme a transação.  
  
 O valor padrão para esta propriedade é zero (0), o que indica que o servidor aguardará indefinidamente. Para obter mais informações sobre propriedades relacionadas a bloqueio, consulte [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 **CoordinatorBuildMaxThreads**  
 Uma propriedade de inteiro de 32 bits assinada que define o número máximo de threads alocados à criação de índices de partição. Aumente esse valor para acelerar a indexação da partição, pelo uso da memória. Para obter mais informações sobre esta propriedade, consulte [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 **CoordinatorCancelCount**  
 Uma propriedade de inteiro de 32 bits assinada que define com que frequência o servidor deve verificar se um evento de cancelamento ocorreu (com base na contagem de iterações internas). Diminua esse número para verificar cancelamentos frequentemente pelo desempenho geral. Essa propriedade é ignorada no modo de servidor tabular.  
  
 **CoordinatorExecutionMode**  
 Uma propriedade de inteiro de 32 bits assinada que define o número máximo de operações paralelas que o servidor tentará, incluindo operações de processamento e consulta. Zero (0) indica que o servidor decidirá, com base em um algoritmo interno. Um número positivo indica o número máximo de operações no total. Um número negativo, com o sinal invertido, indica o número máximo de operações por processador.  

 O valor padrão dessa propriedade é -4, que indica que o servidor está limitado a 4 operações paralelas por processador. Para obter mais informações sobre esta propriedade, consulte [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
 **CoordinatorQueryMaxThreads**  
 Uma propriedade de inteiro de 32 bits assinada que define o número máximo de threads por segmento da partição durante a resolução da consulta. Quanto menor o número de usuários simultâneos, mais alto o valor pode ser, devido ao uso da memória. Inversamente, pode ser necessário baixar o valor se houver um grande número de usuários simultâneos.  
  
 **CoordinatorShutdownMode**  
 Uma propriedade booliana que define modo de desligamento de coordenador. Essa é uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **DataDir**  
 Uma propriedade de cadeia de caracteres que identifica o nome do diretório onde os dados são armazenados.  
  
 **DeploymentMode**  
 Determina o contexto operacional de uma instância de servidor do Analysis Services. Esta propriedade é referenciada como 'modo de servidor' em caixas de diálogo, mensagens e documentação. Esta propriedade é configurada pela Instalação do SQL Server com base no modo de servidor selecionado ao instalar o Analysis Services. Esta propriedade deve ser considerada apenas interna, sempre usando o valor especificado pela Instalação.  
  
 Os valores válidos para essa propriedade incluem os seguintes:  
  
|Value|Descrição|  
|-----------|-----------------|  
|0|Este é o valor padrão. Ele especifica o modo multidimensional, usado para atender bancos de dados multidimensionais que usam o armazenamento MOLAP, HOLAP e ROLAP, bem como modelos de mineração de dados.|  
|1|Especifica instâncias do Analysis Services que foram instaladas como parte de um [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para implantação do SharePoint. Não altere a propriedade de modo de implantação da instância do Analysis Services que faz parte de uma instalação do [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] para SharePoint. [!INCLUDE[ssGemini](../../includes/ssgemini-md.md)] não serão mais executados no servidor se você alterar o modo.|  
|2|Especifica o modo de Tabela usado para hospedar bancos de dados modelo de tabela que usam o armazenamento na memória ou o armazenamento DirectQuery.|  
  
 Cada modo é exclusivo do outro. Um servidor que é configurado para o modo de tabela não pode executar bancos de dados do Analysis Services que contêm cubos e dimensões. Se o hardware subjacente der suporte a isso, você poderá instalar várias instâncias do Analysis Services no mesmo computador e configurar cada instância para usar um modo de implantação diferente. Lembre-se de que o Analysis Services é um aplicativo que utiliza vários recursos. A implantação de várias instâncias no mesmo sistema é recomendada somente para servidores high-end.  
  
 **EnableFast1033Locale**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **ExternalCommandTimeout**  
 Uma propriedade integer que define o tempo limite, em segundos, para comandos emitidos para servidores externos, incluindo fontes de dados relacionais e servidores externos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] .  
  
 O valor padrão desta propriedade é 3600 (segundos).  
  
 **ExternalConnectionTimeout**  
 Uma propriedade de número inteiro que define o tempo limite, em segundos, para criar conexões a servidores externos, incluindo fontes de dados relacionais e servidores externos do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] . Esta propriedade é ignorada quando o tempo limite de uma conexão é especificado na cadeia de conexão.  
  
 O valor padrão desta propriedade é 60 (segundos).  
  
 **ForceCommitTimeout**  
 Uma propriedade integer que especifica quanto tempo, em milissegundos, uma operação de confirmação de gravação deve aguardar para cancelar outros comandos que precederam o comando atual, inclusive consultas em andamento. Isso permite que a transação de confirmação prossiga, cancelando operações de menor prioridade, como consultas.  
  
 O valor padrão desta propriedade é 30 segundos (30000 milissegundos), o que indica que outros comandos serão forçados a atingir o tempo limite até que a transação de confirmação tenha aguardado por 30 segundos.  
  
> [!NOTE]  
>  Consultas e processos cancelados por este evento relatarão a seguinte mensagem de erro: "`Server: The operation has been cancelled`"  
  
 Para obter mais informações sobre esta propriedade, consulte [Guia de Operações do SQL Server 2008 R2 Analysis Services](http://go.microsoft.com/fwlink/?LinkID=225539).  
  
> [!IMPORTANT]  
>  **ForceCommitTimeout** é aplicado para comandos de processamento de cubo e para operações de writeback.  
  
 **IdleConnectionTimeout**  
 Uma propriedade integer que especifica um tempo limite, em segundos, para conexões que estão inativas.  
  
 O valor padrão dessa propriedade é zero (0), que indica que não há tempo limite para conexões ociosas.  
  
 **IdleOrphanSessionTimeout**  
 Uma propriedade integer que define por quanto tempo, em segundos, sessões desligadas serão retidas na memória do servidor. Uma sessão desligada não tem mais uma conexão associada. O padrão é 120 segundos.  
  
 **InstanceVisible**  
 Uma propriedade Booliana que indica se a instância do servidor está visível para descobrir solicitações de instância do serviço do Navegador do SQL Server. O padrão é True. Se você defini-lo como false, a instância não ficará visível para o Navegador do SQL Server.  
  
 **Idioma**  
 Uma propriedade de cadeia de caracteres que define o idioma, inclusive de mensagens de erro e formatação de números. Essa propriedade substitui a propriedade CollationName.  
  
 O valor padrão dessa propriedade é em branco, que indica que a propriedade CollationName define o idioma.  
  
 **LogDir**  
 Uma propriedade de cadeia de caracteres que identifica o nome do diretório que contém os logs de servidor. Essa propriedade só se aplica quando os arquivos do disco são usados para log, em vez de tabelas de banco de dados (o comportamento padrão).  
  
 **MaxIdleSessionTimeout**  
 Uma propriedade integer que define o tempo limite máximo de sessão inativa, em segundos. O padrão é zero (0), indicando que sessões nunca expiram. Entretanto, sessões inativas ainda serão removidas se o servidor tiver restrições de recursos.  
  
 **MinIdleSessionTimeout**  
 Uma propriedade integer que define o tempo mínimo, em segundos, para expiração de sessões inativas. O padrão é 2700 segundos. Depois que esse tempo expirar, o servidor poderá encerrar a sessão ociosa, mas só fará isso se houver necessidade de memória.  
  
 **Porta**  
 Uma propriedade integer que define o número da porta em que o servidor escutará conexões de clientes. Se não definida, o servidor localizará dinamicamente a primeira porta não usada.  
  
 O valor padrão dessa propriedade é zero (0) que, por sua vez, assume a porta 2383 como padrão. Para obter mais informações sobre a configuração da porta, consulte [Configure the Windows Firewall to Allow Analysis Services Access](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md).  
  
 **ServerTimeout**  
 Um integer que define o tempo limite, em segundos, para consultas. O padrão é 3600 segundos (ou 60 minutos). Zero (0) especifica que nenhuma consulta expirará.  
  
 **TempDir**  
 Uma propriedade de cadeia de caracteres que especifica o local para armazenar arquivos temporários usados durante o processamento, a restauração e outras operações. O valor padrão desta propriedade é determinado por configuração. Se não especificado, o padrão será o diretório de Dados.  
  
## <a name="requestprioritization-category"></a>Categoria RequestPrioritization  
 **Ativado**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
 **StatisticsStoreSize**  
 Uma propriedade avançada que não deve ser alterada, exceto sob orientação do suporte da [!INCLUDE[msCoName](../../includes/msconame-md.md)] .  
  
## <a name="see-also"></a>Consulte também  
 [Propriedades do servidor do Analysis Services](../../analysis-services/server-properties/server-properties-in-analysis-services.md)   
 [Determina o Modo de Servidor de uma instância do Analysis Services.](../../analysis-services/instances/determine-the-server-mode-of-an-analysis-services-instance.md)  
  
  
