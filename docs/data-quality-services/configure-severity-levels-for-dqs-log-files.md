---
title: "Configurar n&#237;veis de severidade para arquivos de log do DQS | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "data-quality-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dqs.admin.config.log.f1"
helpviewer_keywords: 
  - "severity levels"
  - "log files,severity levels"
  - "dqs log files,severity levels"
  - "logging,severity levels"
  - "configurar níveis de severidade"
ms.assetid: 66ffcdec-4bf7-4dd5-a221-fd9baefeeef4
caps.latest.revision: 11
author: "JennieHubbard"
ms.author: "jhubbard"
manager: "jhubbard"
caps.handback.revision: 11
---
# Configurar n&#237;veis de severidade para arquivos de log do DQS
  Este tópico descreve como configurar níveis de severidade para várias atividades e módulos no [!INCLUDE[ssDQSnoversion](../includes/ssdqsnoversion-md.md)] (DQS) usando o [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)]. Níveis de severidade definem a intensidade de eventos que ocorrem no DQS. Eventos DQS têm os seguintes níveis de severidade, na ordem decrescente de severidade:  
  
-   **Fatal**: erros de tempo de execução crítico que podem causar resultados severos/inesperados.  
  
-   **Erro**: outros erros em tempo de execução.  
  
-   **Aviso**: avisos sobre eventos que podem resultar em um erro.  
  
-   **Informações**: informações sobre eventos em geral que não são um erro ou um aviso. Por exemplo, um processo de DQS foi iniciado.  
  
-   **Depurar**: (detalhadas) informações detalhadas sobre o evento.  
  
 Ao configurar níveis de severidade para várias atividades e módulos do DQS, você está filtrando as informações a serem registradas e gravando no arquivo de log do DQS para a respectiva atividade ou módulo do DQS. Por exemplo, se você definir o nível de severidade de uma atividade de DQS **Avisar**, apenas aviso e maior gravidade mensagens (erro e Fatal) associadas à atividade do DQS serão registradas.  
  
##  <a name="BeforeYouBegin"></a> Antes de começar  
  
###  <a name="Security"></a> Segurança  
  
####  <a name="Permissions"></a> Permissões  
 É necessário ter a função dqs_administrator no banco de dados DQS_MAIN para configurar definições de severidade de log.  
  
##  <a name="ConfigureActivity"></a> Configurar níveis de severidade em nível de atividade  
 Você pode definir configurações de severidade de log para as seguintes atividades no DQS: gerenciamento de domínio, descoberta de conhecimento, política de correspondência, limpeza de dados, correspondência de dados e serviços de dados de referência. Para fazer isso:  
  
1.  [!INCLUDE[ssDQSInitialStep](../includes/ssdqsinitialstep-md.md)] [Executar o aplicativo de cliente de qualidade de dados](../data-quality-services/run-the-data-quality-client-application.md).  
  
2.  Na tela inicial do [!INCLUDE[ssDQSClient](../includes/ssdqsclient-md.md)] , clique em **Configuração**.  
  
3.  Em seguida, clique o **configurações de Log** guia. As seguintes atividades do DQS são listadas para o qual você pode selecionar um nível de severidade: **gerenciamento de domínio**, **descoberta de Conhecimento**, **o projeto de limpeza (ex. RDS)**, **política de correspondência e projeto de correspondência**, e **RDS**.  
  
4.  Para obter uma atividade do DQS, selecione o nível de severidade a ser registrado. Você pode selecionar uma destas opções: **Fatal**, **Erro**, **Aviso**, **Informações**e **Depuração**. Por exemplo, se você quiser apenas mensagens fatais sejam gravados nos arquivos de log do DQS para a atividade de descoberta de dados de Conhecimento, selecione **Fatal** na lista suspensa em relação a **descoberta de Conhecimento** atividade.  
  
    > [!NOTE]  
    >  Por padrão, **Erro** é selecionado para cada uma das atividades. Isso implica que mensagens de erro e fatais sejam gravadas nos arquivos de log do DQS para cada atividade, por padrão.  
  
5.  Clique em **Fechar**.  
  
##  <a name="ConfigureModule"></a> Configurar níveis de severidade em nível de atividade  
 A seção **Avançado** na guia **Configurações de Log** permite que você defina configurações de severidade de log em um nível de módulo. Módulos são assemblies do sistema DQS que implementam várias funcionalidades em um recurso no DQS. Por exemplo, a atividade de gerenciamento de domínio contém várias funcionalidades, como a definição de regras de domínio, a definição de condições de regra, a definição de regras do domínio cruzado para domínios compostos e assim por diante.  
  
 Às vezes, o nível de granularidade no nível de atividade não é suficiente. Talvez você queira investigar um problema que está ocorrendo em um módulo específico de uma atividade. Convém ter uma opção para configurar severidade de log no nível de módulo para isolar e controlar o problema com mais precisão.  
  
 A configuração de severidade de log especificada no nível de atividade determina a configuração de severidade de log de todos os módulos que constituem a atividade. Entretanto, se houver qualquer conflito entre as configurações de severidade de log nos níveis de atividade e de módulo, as configurações de severidade no nível de módulo serão consideradas.  
  
> [!NOTE]  
>  -   Por padrão, o módulo **Microsoft.Ssdqs.Core.Startup** está pré-configurado na seção **Avançado** com o nível de severidade definido como **Informações**. Isso ocorre para habilitar o log de eventos de severidade Informações e mais alta (Aviso, Erro e Fatal) que estão relacionados ao início e à interrupção de serviços do DQS.  
> -   Você deverá configurar níveis de severidade de log apenas no nível de módulo se for um usuário do DQS avançado que esteja familiarizado com os assemblies do sistema DQS.  
  
 Para configurar níveis de severidade de log no nível de módulo:  
  
1.  Na guia **Configurações de Log** , clique na seta para baixo em **Avançado** para exibir a área.  
  
2.  Na grade que aparece, selecione um nome de módulo da lista suspensa no **módulo** coluna.  
  
3.  Em seguida, selecione um nível de severidade para o módulo da lista suspensa no **gravidade** coluna. Você pode selecionar uma destas opções: **Fatal**, **Erro**, **Aviso**, **Informações**e **Depuração**.  
  
     Por exemplo, na atividade de gerenciamento de domínio, você pode definir um nível de granularidade para a funcionalidade de definição de regra de domínio diferente da atividade de gerenciamento de domínio, selecionando o módulo **Microsoft.Ssdqs.DomainRules.Define** e um nível de severidade de log diferente. Da mesma forma, você pode definir um nível de granularidade diferente para a funcionalidade de regra de domínio cruzado, selecionando o **Microsoft.Ssdqs.DomainRules.Condition.CrossDomain** módulo e selecionando um nível de severidade de log diferente.  
  
4.  Repita as etapas 2 e 3 para outros módulos, caso necessário. Você também pode adicionar ou excluir linhas à grade clicando nos ícones **Adicionar Módulo** e **Remover Módulo** .  
  
5.  Clique em **Fechar**.  
  
## Consulte também  
 [Definir configurações avançadas para arquivos de log do DQS](../data-quality-services/configure-advanced-settings-for-dqs-log-files.md)  
  
  