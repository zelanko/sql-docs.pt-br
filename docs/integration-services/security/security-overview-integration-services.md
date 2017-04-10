---
title: "Vis&#227;o geral de seguran&#231;a (Integration Services) | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Pacotes SSIS, segurança"
  - "Integration Services, segurança"
  - "segurança [Integration Services], sobre a segurança"
  - "senhas [Integration Services]"
  - "pacotes [Integration Services], segurança"
  - "SQL Server Integration Services, segurança"
  - "SSIS, segurança"
  - "Pacotes do Integration Services, segurança"
  - "Pacotes do SQL Server Integration Services, segurança"
ms.assetid: 01aa0b88-d477-4581-9a3b-2efc3de2b133
caps.latest.revision: 73
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 73
---
# Vis&#227;o geral de seguran&#231;a (Integration Services)
  A segurança no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] consiste em várias camadas que fornecem um ambiente de segurança rico e flexível. Estas camadas de segurança incluem o uso de assinaturas digitais, propriedades de pacote, funções de banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e permissões do sistema operacional. A maioria desses recursos de segurança se enquadram nas categorias de identidade e controle de acesso.  
  
## Recursos de identidade  
 Ao implementar recursos de identidade em seus pacotes, você pode alcançar o seguinte objetivo:  
  
 **Você só deve abrir e executar pacotes de fontes confiáveis**.  
  
 Para assegurar que você só abra e execute pacotes de fontes confiáveis, primeiro identifique a fonte dos pacotes. Você pode identificar a fonte assinando pacotes com certificados. Em seguida, quando você abrir ou executar os pacotes, poderá fazer com que o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] verifique a presença e a validade das assinaturas digitais. Para obter mais informações, consulte [Identificar a origem de pacotes com assinaturas digitais](../../integration-services/packages/identify-the-source-of-packages-with-digital-signatures.md).  
  
## Recursos de controle de acesso  
 Ao implementar recursos de identidade em seus pacotes, você pode alcançar o seguinte objetivo:  
  
 **Apenas usuários autorizados devem abrir e executar pacotes**.  
  
 Para assegurar que apenas usuários autorizados abram e executam pacotes, você deve controlar o acesso às seguintes informações:  
  
-   Controle acesso ao conteúdo dos pacotes, principalmente dados confidenciais.  
  
-   Controle o acesso aos pacotes e configurações de pacotes armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Controle o acesso aos pacotes e arquivos relacionados, como configurações, logs e arquivos de ponto de verificação armazenados no sistema de arquivos.  
  
-   Controle o acesso ao serviço [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] e às informações sobre pacotes que o serviço exibe no [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)].  
  
### Controlando o acesso ao conteúdo dos pacotes  
 Para ajudar a restringir o acesso ao conteúdo de um pacote, você pode criptografar pacotes definindo a propriedade ProtectionLevel do pacote. Você pode definir essa propriedade como o nível de proteção necessário para o seu pacote. Por exemplo, em um ambiente de desenvolvimento de equipe, você pode criptografar um pacote usando uma senha conhecida apenas pelos membros da equipe que trabalham no pacote.  
  
 Quando você define a propriedade ProtectionLevel de um pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] detecta automaticamente as propriedades confidenciais e trata essas propriedades de acordo com o nível de proteção do pacote especificado. Por exemplo, defina a propriedade ProtectionLevel de um pacote como um nível que criptografa informações confidenciais com uma senha. Para esse pacote, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criptografa automaticamente os valores de todas as propriedades confidenciais e não exibirá os dados correspondentes sem o fornecimento da senha correta.  
  
 Geralmente, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] identificará as propriedades como confidenciais se elas contiverem informações, como uma senha ou uma cadeia de conexão, ou se essas propriedades corresponderem às variáveis ou aos nós XML gerados por tarefa. Se o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] considera uma propriedade como confidencial, dependerá do desenvolvedor do componente [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , como um gerenciador de conexão ou tarefa, ter designado a propriedade como confidencial. Os usuários não podem adicionar nem remover propriedades da lista de propriedades consideradas confidenciais. Se você escrever tarefas personalizadas, gerenciadores de conexão ou componentes de fluxo de dados, poderá especificar quais propriedades o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] deverá tratar como confidenciais.  
  
 Para obter mais informações, consulte [Access Control for Sensitive Data in Packages](../../integration-services/packages/access-control-for-sensitive-data-in-packages.md).  
  
### Controlando o acesso aos pacotes  
 Você pode salvar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos como arquivos XML que têm a extensão de nome de arquivo .dtsx. Para obter mais informações, consulte [Salvar pacotes](../../integration-services/save-packages.md).  
  
#### Salvando pacotes no banco de dados msdb  
 Salvar os pacotes no banco de dados msdb ajuda a fornecer segurança nos níveis de servidor, banco de dados e tabela. No banco de dados msdb, os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] são armazenados na tabela sysssispackages. Como os pacotes são salvos nas tabelas sysssispackages e sysdtspackages no banco de dados msdb, os pacotes são incluídos no backup automaticamente quando você faz backup do banco de dados msdb.  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os pacotes armazenados no banco de dados msdb também podem ser protegidos com a aplicação das funções no nível de banco de dados do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] inclui três funções fixas em nível do banco de dados, db_ssisadmin, db_ssisltduser e db_ssisoperator, para controlar o acesso aos pacotes. Uma função de leitor e gravador pode estar associada a cada pacote. Também é possível definir funções em nível de banco de dados personalizadas para uso em pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. As funções podem ser implementadas apenas em pacotes salvos no banco de dados msdb em uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Para obter mais informações, veja [Funções do Integration Services &#40;Serviço do SSIS&#41;](../../integration-services/service/integration-services-roles-ssis-service.md).  
  
#### Salvando pacotes no sistema de arquivos  
 Se você armazenar pacotes no sistema de arquivos, em vez de no banco de dados msdb, não se esqueça de proteger os arquivos de pacote e as pastas que contêm arquivos de pacote.  
  
### Controlando o acesso aos arquivos usados por pacotes  
 Os pacotes configurados para usar configurações, pontos de verificação e logs geram informações que são armazenadas fora do pacote. Essas informações podem ser confidenciais e devem ser protegidas. Os arquivos de ponto de verificação podem ser salvos apenas no sistema de arquivos, mas as configurações e os logs podem ser salvos no sistema de arquivos ou nas tabelas em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As configurações e os logs que são salvos no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] estão sujeitos à segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas as informações gravadas no sistema de arquivos requerem segurança adicional.  
  
 Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/access-to-files-used-by-packages.md).  
  
#### Armazenando configurações de pacote com segurança  
 As configurações de pacote podem ser salvas em uma tabela em um banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] ou no sistema de arquivos.  
  
 As configurações podem ser salvas em qualquer banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], não só no banco de dados msdb. Assim, você pode especificar qual banco de dados atua como o repositório de configurações de pacote. Você também pode especificar o nome da tabela que conterá as configurações e o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criará a tabela automaticamente com a estrutura correta. Salvar as configurações em uma tabela permite fornecer segurança nos níveis de servidor, banco de dados e tabela. Além disso, as configurações que são salvas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] são automaticamente incluídas no backup do banco de dados.  
  
 Se você não armazenar configurações no sistema de arquivos, em vez de no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], proteja as pastas no sistema de arquivos que contenham os arquivos de configuração de pacote.  
  
 Para obter mais informações sobre configurações, consulte [Package Configurations](../../integration-services/packages/package-configurations.md).  
  
### Controlando o acesso ao serviço Integration Services  
 [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] usa o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para listar pacotes armazenados. Para impedir que usuários não autorizados exibam informações sobre pacotes armazenados em computadores locais e remotos, e, assim, obtenham informações privadas, restrinja o acesso aos computadores que executam o serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
 Para obter mais informações, consulte [Acesso ao serviço Integration Services](../../integration-services/security/access-to-the-integration-services-service.md).  
  
## Tarefas relacionadas  
 A lista a seguir contém links para tópicos que mostram como executar uma determinada tarefa relativa à segurança.  
  
-   [Criar uma função definida pelo usuário](../../integration-services/service/create-a-user-defined-role.md)  
  
-   [Atribuir uma função de leitor e de gravador a um pacote](../../integration-services/service/assign-a-reader-and-writer-role-to-a-package.md)  
  
-   [Implementar uma política de assinatura por meio da configuração de um valor do Registro](../../integration-services/packages/implement-a-signing-policy-by-setting-a-registry-value.md)  
  
-   [Assinar um pacote por meio de um certificado digital](../../integration-services/packages/sign-a-package-by-using-a-digital-certificate.md)  
  
-   [Definir ou alterar o nível de proteção de pacotes](../../integration-services/packages/set-or-change-the-protection-level-of-packages.md)  
  
## Consulte também  
 [SQL Server Integration Services](../../integration-services/sql-server-integration-services.md)  
  
  