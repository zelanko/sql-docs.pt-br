---
title: "Implantar projetos e pacotes do Integration Services (SSIS) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
ms.assetid: bea8ce8d-cf63-4257-840a-fc9adceade8c
caps.latest.revision: 21
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 21
---
# Implantar projetos e pacotes do Integration Services (SSIS)
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] dá suporte a dois modelos de implantação, o modelo de implantação de projeto e o modelo de implantação de pacote herdado. O modelo de implantação de projeto permite que você implante seus projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
 Para obter mais informações sobre implantação de projetos no servidor do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], consulte [Implantar projetos no servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md).  
  
 Para obter mais informações sobre o modelo de implantação de pacote herdado, consulte [Implantação de pacote herdado &#40;SSIS&#41;](../../integration-services/packages/legacy-package-deployment-ssis.md).  
  
> [!NOTE]  
>  O modelo de implantação do projeto foi introduzido no [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]. Ao usar esse modelo, você não conseguia implantar um ou mais pacotes sem implantar o projeto inteiro. O [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] introduziu o recurso de Implantação Incremental de Pacotes que permite implantar um ou mais pacotes, sem implantar o projeto inteiro. Consulte [Implantar pacotes no Integration Services Server](../../integration-services/packages/deploy-packages-to-integration-services-server.md) para ver mais detalhes sobre esse recurso.  
  
## Compare o modelo de implantação de projeto e o modelo de implantação de pacote herdado  
 O tipo de modelo de implantação que você escolhe para um projeto determina quais opções de desenvolvimento e administrativas estão disponíveis para aquele projeto. A tabela a seguir mostra as diferenças e as semelhanças entre o uso do modelo de implantação de projeto e o uso do modelo de implantação de pacote.  
  
|Ao usar o modelo de implantação de projeto|Quando usar o modelo de implantação de pacote herdado|  
|---------------------------------------------|----------------------------------------------------|  
|Um projeto é a unidade de implantação.|Um pacote é a unidade de implantação.|  
|Parâmetros são usados para atribuir valores a propriedades de pacote.|As configurações são usadas para atribuir valores a propriedades de pacote.|  
|Um projeto, que contém pacotes e parâmetros, é compilado em um arquivo de implantação de projeto (extensão .ispac).|Os pacotes (extensão .dtsx) e as configurações (extensão .dtsConfig) são salvos individualmente no sistema de arquivos.|  
|Um projeto que contém pacotes e parâmetros é implantado no catálogo do SSISDB em uma instância do SQL Server.|Os pacotes e as configurações são copiados no sistema de arquivos em outro computador. Os pacotes também podem ser salvos no banco de dados MSDB ou em uma instância do SQL Server.|  
|A integração CLR é necessária no mecanismo de banco de dados.|A integração CLR não é necessária no mecanismo de banco de dados.|  
|Os valores dos parâmetros específicos ao ambiente são armazenados em variáveis de ambiente.|Os valores de configuração específicos ao ambiente são armazenados nos arquivos de configuração.|  
|Os projetos e pacotes do catálogo podem ser validados no servidor antes da execução. Você pode usar o SQL Server Management Studio, procedimentos armazenados ou código gerenciado para executar a validação.|Os pacotes são validados antes da execução. Você também pode validar um pacote com o código gerenciado dtExec.|  
|Os pacotes são executados com o início de uma execução no mecanismo de banco de dados. Um identificador de projeto, valores de parâmetros explícitos (opcional) e referências ao ambiente (opcional) são atribuídos a uma execução antes de ela ser iniciada.<br /><br /> Também é possível executar pacotes usando **dtExec**.|Os pacotes são executados com os utilitários de execução **dtExec** e **DTExecUI**. As configurações aplicáveis são identificadas por argumentos de prompt de comando (opcional).|  
|Durante a execução, os eventos produzidos pelo pacote são capturados automaticamente e salvos no catálogo. Você pode consultar esses eventos com exibições Transact-SQL.|Durante a execução, os eventos produzidos por um pacote não são capturados automaticamente. Um provedor de log deve ser adicionado ao pacote para capturar eventos.|  
|Os pacotes são executados em um processo separado do Windows.|Os pacotes são executados em um processo separado do Windows.|  
|O SQL Server Agent é usado para agendar a execução do pacote.|O SQL Server Agent é usado para agendar a execução do pacote.|  
  
 O modelo de implantação do projeto foi introduzido no [!INCLUDE[ssISversion11](../../includes/ssisversion11-md.md)]. Ao usar esse modelo, você não conseguia implantar um ou mais pacotes sem implantar o projeto inteiro. O [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] introduziu o recurso de Implantação Incremental de Pacotes que permite implantar um ou mais pacotes, sem implantar o projeto inteiro. Consulte [Implantar pacotes no Integration Services Server](../../integration-services/packages/deploy-packages-to-integration-services-server.md) para ver mais detalhes sobre esse recurso.  
  
## Recursos do modelo de implantação de projeto  
 A tabela a seguir lista os recursos que estão disponíveis para projetos desenvolvidos apenas para o modelo de implantação de projeto.  
  
|Recurso|Description|  
|-------------|-----------------|  
|Parâmetros|Um parâmetro especifica os dados que serão usados por um pacote. Você pode definir o escopo dos parâmetros no nível do pacote ou do projeto com parâmetros de pacote e de projeto, respectivamente. Os parâmetros podem ser usados em expressões ou tarefas. Quando o projeto é implantado no catálogo, você pode atribuir um valor literal para cada parâmetro ou usar o valor padrão que foi atribuído em tempo de design. Em lugar de um valor literal, você também pode fazer referência a uma variável de ambiente. Os valores de variáveis de ambiente são resolvidos na hora da execução do pacote.|  
|Ambientes|Um ambiente é um contêiner de variáveis que podem ser referenciadas por projetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Cada projeto pode ter várias referências de ambiente, mas uma única instância de execução de pacote pode fazer referência apenas a variáveis de um único ambiente. Os ambientes permitem organizar os valores que você atribui a um pacote. Por exemplo, você pode ter ambientes denominados "Desenvolvimento", "Teste" e "Produção".|  
|Variáveis de ambiente|Uma variável de ambiente define um valor literal que pode ser atribuído a um parâmetro durante a execução do pacote. Para usar uma variável de ambiente, crie uma referência de ambiente (no projeto que corresponde ao ambiente que tem o parâmetro), atribua um valor de parâmetro ao nome da variável de ambiente e especifique a referência de ambiente correspondente ao configurar uma instância de execução.|  
|Catálogo do SSISDB|Todos os objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenados e gerenciados em uma instância do SQL Server em um banco de dados chamado de catálogo do SSISDB. O catálogo permite usar pastas para organizar seus projetos e ambientes. Cada instância do SQL Server pode ter um catálogo. Cada catálogo pode ter zero ou mais pastas. Cada pasta pode ter zero ou mais projetos e zero ou mais ambientes. Uma pasta do catálogo também pode ser usada como um limite para permissões para objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].|  
|Procedimentos armazenados e exibições do catálogo|Um grande número de procedimentos armazenados e exibições pode ser usado para gerenciar objetos do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no catálogo. Por exemplo, você pode especificar valores para parâmetros e variáveis de ambiente, criar e iniciar execuções e monitorar operações do catálogo. É possível até ver exatamente quais valores serão usados por um pacote antes do início da execução.|  
  
## Implantação de projeto  
 No centro do modelo de implantação do projeto está o arquivo de implantação do projeto (extensão .ispac). O arquivo de implantação do projeto é uma unidade independente de implantação que inclui apenas as informações essenciais sobre os pacotes e parâmetros do projeto. O arquivo de implantação do projeto não captura todas as informações contidas no arquivo do projeto do Integration Services (extensão .dtproj). Por exemplo, arquivos de texto adicionais que você usa para escrever observações não são armazenados no arquivo de implantação do projeto e, portanto, não são implantados no catálogo.  
  
## Tarefas necessárias  
  
-   [Implantar projetos no Servidor do Integration Services](../../integration-services/packages/deploy-projects-to-integration-services-server.md)  
  
## Conteúdo relacionado  
 Entrada de blog [Ideias sobre estratégias de expansão para projetos do SSIS](http://go.microsoft.com/fwlink/?LinkId=245739) em mattmasson.com.  
  
## Consulte também  
 [Utilitário dtexec](../../integration-services/packages/dtexec-utility.md)  
  
  