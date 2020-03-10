---
title: Visão geral de segurança (Integration Services) | Microsoft Docs
ms.custom: security
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- SSIS packages, security
- Integration Services, security
- security [Integration Services], about security
- passwords [Integration Services]
- packages [Integration Services], security
- SQL Server Integration Services, security
- SSIS, security
- Integration Services packages, security
- SQL Server Integration Services packages, security
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 0bc268c2baea6e0e661fac123df9fe19ec60252c
ms.sourcegitcommit: ff1bd69a8335ad656b220e78acb37dbef86bc78a
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/05/2020
ms.locfileid: "78338869"
---
# <a name="security-overview-integration-services"></a>Visão geral de segurança (Integration Services)

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


  A segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consiste em várias camadas que fornecem um ambiente de segurança avançado e flexível. Estas camadas de segurança incluem o uso de assinaturas digitais, propriedades de pacote, funções de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permissões do sistema operacional. A maioria desses recursos de segurança se enquadram nas categorias de identidade e controle de acesso.  

## <a name="threat-and-vulnerability-mitigation"></a>Redução de ameaças e vulnerabilidades
  Embora o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclua diversos mecanismos de segurança, os pacotes e os arquivos criados ou utilizados por pacotes podem ser explorados com más intenções.  
  
 A tabela a seguir descreve esses riscos e as etapas proativas que você pode executar para diminuí-los.  
  
|Ameaça ou vulnerabilidade|Definição|Atenuação|  
|-----------------------------|----------------|----------------|  
|Origem do pacote|A origem de um pacote é a pessoa ou organização que criou o pacote. Pode ser arriscado executar um pacote de origem desconhecida ou não confiável.|Identifique a origem do pacote usando uma assinatura digital e apenas execute pacotes provenientes de fontes conhecidas e confiáveis. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).|  
|Conteúdo do pacote|O conteúdo de um pacote inclui os elementos do pacote e suas propriedades. As propriedades podem conter dados confidenciais, como uma senha ou uma cadeia de conexão. Elementos de pacote como uma instrução SQL podem revelar a estrutura de seu banco de dados.|Para controlar o acesso a um pacote e ao seu conteúdo, execute as seguintes etapas:<br /><br /> 1) Para controlar o acesso ao pacote propriamente dito, aplique recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] aos pacotes salvos no banco de dados **msdb** em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Aos pacotes salvos no sistema de arquivos, aplique os recursos de segurança do sistema de arquivos, como ACLs (listas de controle de acesso).<br /><br /> 2) Para controlar o acesso aos conteúdos do pacote, defina o nível de proteção do pacote.<br /><br /> Para obter mais informações, consulte [Visão geral de segurança &#40;Integration Services&#41;](../../integration-services/security/security-overview-integration-services.md) e [Controle de acesso de dados confidenciais em pacotes](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).|  
|Saída do pacote|Quando você configura um pacote para usar configurações, pontos de verificação e log, o pacote armazena essas informações fora dele. As informações armazenadas fora do pacote pode conter dados confidenciais.|Para proteger as configurações e os logs que o pacote salva em tabelas de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , use os recursos de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .<br /><br /> Para controlar o acesso a arquivos, use as ACLs disponíveis no sistema de arquivos.<br /><br /> Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](#files)|  
  
## <a name="identity-features"></a>Recursos de identidade  
 Ao implementar recursos de identidade em seus pacotes, você pode alcançar o seguinte objetivo:  
  
 **Você só deve abrir e executar pacotes de fontes confiáveis**.  
  
 Para assegurar que você só abra e execute pacotes de fontes confiáveis, primeiro identifique a fonte dos pacotes. Você pode identificar a fonte assinando pacotes com certificados. Em seguida, quando você abrir ou executar os pacotes, poderá fazer com que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a presença e a validade das assinaturas digitais. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md).  
  
## <a name="access-control-features"></a>Recursos de controle de acesso  
 Ao implementar recursos de identidade em seus pacotes, você pode alcançar o seguinte objetivo:  
  
 **Apenas usuários autorizados devem abrir e executar pacotes**.  
  
 Para assegurar que apenas usuários autorizados abram e executam pacotes, você deve controlar o acesso às seguintes informações:  
  
-   Controle acesso ao conteúdo dos pacotes, principalmente dados confidenciais.  
  
-   Controle o acesso aos pacotes e configurações de pacotes armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Controle o acesso aos pacotes e arquivos relacionados, como configurações, logs e arquivos de ponto de verificação armazenados no sistema de arquivos.  
  
-   Controle o acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e às informações sobre pacotes que o serviço exibe no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### <a name="controlling-access-to-the-contents-of-packages"></a>Controlando o acesso ao conteúdo dos pacotes  
 Para ajudar a restringir o acesso ao conteúdo de um pacote, você pode criptografar pacotes definindo a propriedade ProtectionLevel do pacote. Você pode definir essa propriedade como o nível de proteção necessário para o seu pacote. Por exemplo, em um ambiente de desenvolvimento de equipe, você pode criptografar um pacote usando uma senha conhecida apenas pelos membros da equipe que trabalham no pacote.  
  
 Quando você define a propriedade ProtectionLevel de um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] detecta automaticamente as propriedades confidenciais e trata essas propriedades de acordo com o nível de proteção do pacote especificado. Por exemplo, defina a propriedade ProtectionLevel de um pacote como um nível que criptografa informações confidenciais com uma senha. Para esse pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criptografa automaticamente os valores de todas as propriedades confidenciais e não exibirá os dados correspondentes sem o fornecimento da senha correta.  
  
 Geralmente, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] identificará as propriedades como confidenciais se elas contiverem informações, como uma senha ou uma cadeia de conexão, ou se essas propriedades corresponderem às variáveis ou aos nós XML gerados por tarefa. Se o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] considera uma propriedade como confidencial, dependerá do desenvolvedor do componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como um gerenciador de conexão ou tarefa, ter designado a propriedade como confidencial. Os usuários não podem adicionar nem remover propriedades da lista de propriedades consideradas confidenciais. Se você escrever tarefas personalizadas, gerenciadores de conexão ou componentes de fluxo de dados, poderá especificar quais propriedades o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deverá tratar como confidenciais.  
  
 Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../../integration-services/security/access-control-for-sensitive-data-in-packages.md).  
  
### <a name="controlling-access-to-packages"></a>Controlando o acesso aos pacotes  
 Você pode salvar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou no sistema de arquivos como arquivos XML que têm a extensão de nome de arquivo .dtsx. Para obter mais informações, consulte [Salvar pacotes](../../integration-services/save-packages.md).  
  
#### <a name="saving-packages-to-the-msdb-database"></a>Salvando pacotes no banco de dados msdb  
 Salvar os pacotes no banco de dados msdb ajuda a fornecer segurança nos níveis de servidor, banco de dados e tabela. No banco de dados msdb, os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenados na tabela sysssispackages. Como os pacotes são salvos nas tabelas sysssispackages e sysdtspackages no banco de dados msdb, os pacotes são incluídos no backup automaticamente quando você faz backup do banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os pacotes armazenados no banco de dados msdb também podem ser protegidos com a aplicação das funções no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui três funções fixas em nível do banco de dados, db_ssisadmin, db_ssisltduser e db_ssisoperator, para controlar o acesso aos pacotes. Uma função de leitor e gravador pode estar associada a cada pacote. Também é possível definir funções em nível de banco de dados personalizadas para uso em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] . As funções podem ser implementadas apenas em pacotes salvos no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/security/integration-services-roles-ssis-service.md).  
  
#### <a name="saving-packages-to-the-file-system"></a>Salvando pacotes no sistema de arquivos  
 Se você armazenar pacotes no sistema de arquivos, em vez de no banco de dados msdb, não se esqueça de proteger os arquivos de pacote e as pastas que contêm arquivos de pacote.  
  
### <a name="controlling-access-to-files-used-by-packages"></a>Controlando o acesso aos arquivos usados por pacotes  
 Os pacotes configurados para usar configurações, pontos de verificação e logs geram informações que são armazenadas fora do pacote. Essas informações podem ser confidenciais e devem ser protegidas. Os arquivos de ponto de verificação podem ser salvos apenas no sistema de arquivos, mas as configurações e os logs podem ser salvos no sistema de arquivos ou nas tabelas em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As configurações e os logs que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão sujeitos à segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas as informações gravadas no sistema de arquivos requerem segurança adicional.  
  
 Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](#files).  
  
#### <a name="storing-package-configurations-securely"></a>Armazenando configurações de pacote com segurança  
 As configurações de pacote podem ser salvas em uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 As configurações podem ser salvas em qualquer banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , não só no banco de dados msdb. Assim, você pode especificar qual banco de dados atua como o repositório de configurações de pacote. Você também pode especificar o nome da tabela que conterá as configurações e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará a tabela automaticamente com a estrutura correta. Salvar as configurações em uma tabela permite fornecer segurança nos níveis de servidor, banco de dados e tabela. Além disso, as configurações que são salvas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são automaticamente incluídas no backup do banco de dados.  
  
 Se você não armazenar configurações no sistema de arquivos, em vez de no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proteja as pastas no sistema de arquivos que contenham os arquivos de configuração de pacote.  
  
 Para obter mais informações sobre configurações, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### <a name="controlling-access-to-the-integration-services-service"></a>Controlando o acesso ao serviço Integration Services  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para listar pacotes armazenados. Para impedir que usuários não autorizados exibam informações sobre pacotes armazenados em computadores locais e remotos, e, assim, obtenham informações privadas, restrinja o acesso aos computadores que executam o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Acesso ao serviço Integration Services](#service).  

## <a name="files"></a> Acesso aos arquivos usados por pacotes
  O nível de proteção do pacote não protege arquivos armazenados fora do pacote. Esses arquivos incluem o seguinte:  
  
-   Arquivos de configuração  
  
-   arquivos de ponto de verificação  
  
-   Arquivos de log  
  
 Esses arquivos devem ser protegidos separadamente, especialmente se eles incluírem informações confidenciais.  
  
### <a name="configuration-files"></a>Arquivos de configuração  
 Se você tiver informações confidenciais em uma configuração, como informações de logon e senha, deverá salvar a configuração no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]ou usar uma ACL (lista de controle de acesso), para restringir acesso ao local ou à pasta na qual você armazena os arquivos e só permitir o acesso a determinadas contas. Normalmente, você concede acesso às contas que você permite que executem pacotes, e às contas que gerenciam e solucionam problemas de pacotes, que podem incluir revisão do conteúdo de configuração, ponto de verificação e arquivos de log. [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece o armazenamento mais seguro porque oferece proteção nos níveis de servidor e de banco de dados. Para salvar configurações no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], use o tipo de configuração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para salvar no sistema de arquivos, use o tipo de configuração XML.  
  
 Para obter mais informações, consulte [Configurações de pacote](../../integration-services/packages/package-configurations.md), [Criar configurações de pacote](../../integration-services/packages/create-package-configurations.md)e [Considerações de segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md).  
  
### <a name="checkpoint-files"></a>arquivos de ponto de verificação  
 Do mesmo modo, se o arquivo de ponto de verificação usado pelo pacote incluir informações confidenciais, você deverá usar uma lista de controle de acesso (ACL) para proteger o local ou a pasta onde armazena o arquivo. Arquivos de ponto de verificação salvam informações do estado atual no andamento do pacote, bem como os valores atuais das variáveis. Por exemplo, o pacote pode incluir uma variável personalizada que contenha um número de telefone. Para saber mais, confira [Restart Packages by Using Checkpoints](../../integration-services/packages/restart-packages-by-using-checkpoints.md).  
  
### <a name="log-files"></a>Arquivos de log  
 As entradas de log que são gravadas no sistema de arquivos também devem ser protegidas usando uma lista de controle de acesso (ACL). As entradas de log também podem ser armazenadas em tabelas do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e protegidas pela segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As entradas de logs podem incluir informações confidenciais, por exemplo, se o pacote contiver uma tarefa Executar SQL que cria uma instrução SQL referente a um número de telefone, a entrada de log para a instrução SQL incluirá o número de telefone. A instrução SQL também pode revelar informações particulares sobre nomes de tabelas e colunas nos bancos de dados. Para obter mais informações, consulte [Log do SSIS &#40;Integration Services&#41;](../../integration-services/performance/integration-services-ssis-logging.md).  

## <a name="service"></a> Acesso ao serviço Integration Services
  Os níveis de proteção do pacote podem limitar quem tem permissão para editar e executar um pacote. É necessário ter proteção adicional para limitar quem pode exibir a lista de pacotes que estão sendo executados em um servidor e quem pode interromper a execução de pacotes no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para listar os pacotes em execução. Os membros do grupo Administradores do Windows podem visualizar e parar todos os pacotes em execução. Os usuários que não são membros do grupo Administradores podem visualizar e parar apenas os pacotes iniciados por eles.  
  
 É importante restringir o acesso a computadores que executam um serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , especialmente um serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que pode enumerar pastas remotas. Qualquer usuário autenticado pode solicitar a enumeração dos pacotes. Mesmo se o serviço não localizar o serviço, ele enumerará as pastas. Esses nomes de pastas podem ser úteis a um usuário mal-intencionados. Se um administrador tiver configurado o serviço para enumerar pastas em uma máquina remota, os usuários também poderão ver os nomes de pastas que eles normalmente não conseguiriam consultar.  

## <a name="related-tasks"></a>Related Tasks  
 A lista a seguir contém links para tópicos que mostram como executar uma determinada tarefa relativa à segurança.  
  
-   [Criar uma função definida pelo usuário](../../integration-services/security/integration-services-roles-ssis-service.md#create)  
  
-   [Atribuir uma função de leitor e de gravador a um pacote](../../integration-services/security/integration-services-roles-ssis-service.md#assign)  
  
-   [Implementar uma política de assinatura por meio da configuração de um valor do Registro](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#registry)  
  
-   [Assinar um pacote por meio de um certificado digital](../../integration-services/security/identify-the-source-of-packages-with-digital-signatures.md#cert)  
  
-   [Definir ou alterar o nível de proteção de pacotes](../../integration-services/security/access-control-for-sensitive-data-in-packages.md#set_protection)  
