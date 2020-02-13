---
title: Visão geral de DevOps do SQL Server Integration Services | Microsoft Docs
description: Saiba como criar a CI/CD do SSIS com as Ferramentas de DevOps do SSIS.
ms.date: 12/06/2019
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 88b8e54867aba5439af9ed87e4a42b2083a479b3
ms.sourcegitcommit: b2e81cb349eecacee91cd3766410ffb3677ad7e2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/01/2020
ms.locfileid: "76281864"
---
# <a name="sql-server-integration-services-ssis-devops-tools-preview"></a>Ferramentas de DevOps do SSIS (SQL Server Integration Services) (versão prévia)

A extensão [Ferramentas de DevOps do SSIS](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) está disponível no marketplace do **Azure DevOps**.

Caso você não tenha uma organização do **Azure DevOps**, primeiro, inscreva-se no [Azure Pipelines](https://docs.microsoft.com/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops) e, em seguida, adicione a extensão **Ferramentas de DevOps do SSIS** seguindo [as etapas](https://docs.microsoft.com/azure/devops/marketplace/overview?view=azure-devops&tabs=browser#add-an-extension).

As **Ferramentas de DevOps do SSIS** incluem a tarefa **Build do SSIS** e a tarefa de versão **Implantação do SSIS**.

- A tarefa **Build do SSIS** dá suporte à criação de arquivos dtproj no modelo de implantação de projeto ou no modelo de implantação de pacote.

- A tarefa **Implantação do SSIS** dá suporte à implantação de arquivos ispac únicos ou múltiplos no catálogo local do SSIS e no Azure-SSIS IR ou arquivos SSISDeploymentManifest e os arquivos associados localmente ou no compartilhamento de arquivo do Azure.

## <a name="ssis-build-task"></a>Tarefa Build do SSIS

![tarefa de build](media/ssis-build-task.png)

### <a name="properties"></a>Propriedades

#### <a name="project-path"></a>Caminho do projeto

Caminho da pasta do projeto ou do arquivo a ser compilado. Se um caminho de pasta for especificado, a tarefa Build do SSIS pesquisará todos os arquivos dtproj de maneira recursiva nessa pasta e os criará.

#### <a name="project-configuration"></a>Configuração do projeto

Nome da configuração de projeto a ser usada para o build. Se ele não for fornecido, usará como padrão a primeira configuração de projeto definida em cada arquivo dtproj.

#### <a name="output-path"></a>Caminho de saída

Caminho de uma pasta separada para salvar os resultados do build, que podem ser publicados como artefatos de compilação por meio da tarefa [publicar artefatos de compilação](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops).

### <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

- A tarefa Build do SSIS depende do Visual Studio e do Designer SSIS, que é obrigatório nos agentes de build. Portanto, para executar a tarefa Build do SSIS no pipeline, escolha **vs2017-win2016** para agentes hospedados pela Microsoft ou instale o Visual Studio e o Designer SSIS (VS2017 + SSDT2017 ou VS2019 + extensão Projetos do SSIS) em agentes auto-hospedados.

- Para criar projetos do SSIS usando componentes prontos para uso (incluindo o feature pack do SSIS para o Azure e outros componentes de terceiros), os componentes prontos para uso precisam ser instalados no computador em que o agente de pipeline está em execução.  Para o agente hospedado pela Microsoft, o usuário pode adicionar uma [tarefa Script do PowerShell](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) ou uma [tarefa Script de Linha de Comando](https://docs.microsoft.com/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops) para baixar e instalar os componentes antes de executar a tarefa Build do SSIS.

- Não há suporte para o nível de proteção **EncryptSensitiveWithPassword** e **EncryptAllWithPassword** na tarefa Build do SSIS. Verifique se todos os projetos do SSIS na base de código não estão usando esses dois níveis de proteção ou a tarefa Build do SSIS será suspensa e atingirá o tempo limite durante a execução.

## <a name="ssis-deploy-task"></a>Tarefa Implantação do SSIS

![tarefa de implantação](media/ssis-deploy-task.png)

### <a name="properties"></a>Propriedades

#### <a name="source-path"></a>Caminho de origem

O caminho dos arquivos ISPAC ou SSISDeploymentManifest de origem que você deseja implantar. Esse caminho pode ser um caminho de pasta ou um caminho de arquivo.

#### <a name="destination-type"></a>Tipo de destino

Tipo do destino. Atualmente, a tarefa Implantação do SSIS dá suporte a dois tipos:

- *Sistema de arquivos*: Implante arquivos SSISDeploymentManifest e os arquivos associados em um sistema de arquivos especificado. Há suporte para o compartilhamento de arquivo local e do Azure.
- *SSISDB*: Implante arquivos ISPAC em um catálogo do SSIS especificado, que pode ser hospedado no SQL Server local ou no Azure-SSIS Integration Runtime.

#### <a name="destination-server"></a>Servidor de destino

Nome do SQL Server de destino. Pode ser o nome de um SQL Server local, de um Banco de Dados SQL do Azure ou de uma Instância Gerenciada do Banco de Dados SQL do Azure. Essa propriedade só é visível quando o tipo de destino é SSISDB.

#### <a name="destination-path"></a>Caminho de destino

Caminho da pasta de destino no qual o arquivo de origem será implantado. Por exemplo:

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

A tarefa Implantação do SSIS criará a pasta e a subpasta caso elas não existam.

#### <a name="authentication-type"></a>Tipo de autenticação

Tipo de autenticação para acessar o servidor de destino especificado. Essa propriedade só é visível quando o tipo de destino é SSISDB. Em geral, a tarefa Implantação do SSIS dá suporte a quatro tipos:

- Autenticação do Windows
- Autenticação do SQL Server
- Active Directory – Senha
- Active Directory – Integrado

Porém, o suporte ao tipo de autenticação específico depende do tipo de servidor de destino e do tipo de agente. A matriz de suporte detalhado é listada na tabela abaixo.

| |Agente hospedado pela Microsoft|Agente auto-hospedado|
|---------|---------|---------|
|SQL Server local ou VM |N/D|Autenticação do Windows|
|SQL do Azure|Autenticação do SQL Server <br> Active Directory – Senha|Autenticação do SQL Server <br> Active Directory – Senha <br> Active Directory – Integrado|

#### <a name="domain-name"></a>Nome de domínio

Nome de domínio para acessar o sistema de arquivos especificado. Essa propriedade só é visível quando o tipo de destino é sistema de arquivos.
Você poderá deixá-la vazia quando a conta de usuário usada para executar o agente auto-hospedado receber acesso de leitura/gravação ao caminho de destino especificado.

#### <a name="username"></a>Nome de Usuário

Nome de usuário para acessar o SSISDB ou o sistema de arquivos especificado. Essa propriedade é visível quando o tipo de destino é sistema de arquivos ou o tipo de autenticação é Autenticação do SQL Server ou Active Directory: senha.
Você poderá deixá-la vazia quando o tipo de destino for sistema de arquivos e a conta de usuário usada para executar o agente auto-hospedado receber acesso de leitura/gravação ao caminho de destino especificado.

#### <a name="password"></a>Senha

Senha para acessar o SSISDB ou o sistema de arquivos especificado. Essa propriedade é visível quando o tipo de destino é sistema de arquivos ou o tipo de autenticação é Autenticação do SQL Server ou Active Directory: senha.
Você poderá deixá-la vazia quando o tipo de destino for sistema de arquivos e a conta de usuário usada para executar o agente auto-hospedado receber acesso de leitura/gravação ao caminho de destino especificado.

#### <a name="overwrite-existing-projects-or-ssisdeploymentmanifest-files-of-the-same-names"></a>Substituir projetos existentes ou arquivos SSISDeploymentManifest com os mesmos nomes

Especifique se deseja substituir os projetos existentes ou os arquivos SSISDeploymentManifest com os mesmos nomes. Se a opção for 'Não', a tarefa Implantação do SSIS vai ignorar a implantação desses projetos ou desses arquivos.

#### <a name="continue-deployment-when-error-occurs"></a>Continuar a implantação quando ocorrer um erro

Especifique se a implantação continuará para projetos ou arquivos restantes quando ocorrer um erro. Se a opção for 'Não', a tarefa Implantação do SSIS será interrompida imediatamente quando ocorrer um erro.

### <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

Atualmente, a tarefa Implantação do SSIS não dá suporte aos seguintes cenários:

- Configurar o ambiente no catálogo do SSIS.
- Implantar o ispac no Azure SQL Server ou na Instância Gerenciada do Azure SQL que só permite a MFA (autenticação multifator).
- Implantar pacotes no Repositório de Pacotes SSIS ou no MSDB.

## <a name="release-notes"></a>Notas de versão

### <a name="version-013-preview"></a>Versão 0.1.3 Versão prévia

Data de lançamento: 19 de janeiro de 2020

- Corrigido um problema que impedia a implantação do ispac quando seu nome de arquivo original era alterado.

### <a name="version-012-preview"></a>Versão 0.1.2 Versão prévia

Data de lançamento: 13 de janeiro de 2020

- Foram adicionadas informações de exceção mais detalhadas no log da tarefa de implantação do SSIS quando o tipo de destino é SSISDB.
- Foi corrigido o caminho de destino de exemplo no texto de ajuda do caminho de destino da propriedade da tarefa de implantação do SSIS.

### <a name="version-011-preview"></a>Versão 0.1.1 versão prévia

Data de lançamento: 6 de janeiro de 2020

- Foi adicionada uma restrição do requisito mínimo de versão do agente. Atualmente, a versão mínima do agente deste produto é 2.144.0.
- Foram corrigidos alguns textos de exibição incorretos para a tarefa de implantação do SSIS.
- Refinamento de algumas mensagens de erro.

### <a name="version-010-preview"></a>Versão 0.1.0 Versão prévia

Data de lançamento: 5 de dezembro de 2019

Versão inicial das Ferramentas de DevOps do SSIS. Essa é uma versão prévia.

## <a name="next-steps"></a>Próximas etapas

- Obter a [extensão DevOps do SSIS](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools)
