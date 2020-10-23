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
ms.openlocfilehash: 1cc68be44a45ece8ad844585162b0cff651ae487
ms.sourcegitcommit: cfa04a73b26312bf18d8f6296891679166e2754d
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/19/2020
ms.locfileid: "92194079"
---
# <a name="sql-server-integration-services-ssis-devops-tools-azure-devops-extension"></a>Extensão do Azure DevOps para Ferramentas de DevOps do SSIS (SQL Server Integration Services)

A extensão [Ferramentas de DevOps do SSIS](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools) está disponível no Marketplace do **Azure DevOps**.

Caso você não tenha uma organização do **Azure DevOps**, primeiro, inscreva-se no [Azure Pipelines](/azure/devops/pipelines/get-started/pipelines-sign-up?view=azure-devops) e, em seguida, adicione a extensão **Ferramentas de DevOps do SSIS** seguindo [as etapas](/azure/devops/marketplace/overview?tabs=browser&view=azure-devops#add-an-extension).

As **Ferramentas de DevOps do SSIS** incluem a tarefa **Build do SSIS**, tarefa de versão **Implantação do SSIS** e a **tarefa de Configuração de Catálogo do SSIS**.

- A tarefa **[Build do SSIS](#ssis-build-task)** dá suporte à criação de arquivos dtproj no modelo de implantação de projeto ou no modelo de implantação de pacote.

- A tarefa **[Implantação do SSIS](#ssis-deploy-task)** dá suporte à implantação de arquivos ispac únicos ou múltiplos no catálogo local do SSIS e no Azure-SSIS IR ou arquivos SSISDeploymentManifest e os arquivos associados localmente ou no compartilhamento de arquivo do Azure.

- A tarefa **[Configuração de Catálogo do SSIS](#ssis-catalog-configuration-task)** dá suporte à configuração de pasta/projeto/ambiente do Catálogo do SSIS com um arquivo de configuração no formato JSON. Essa tarefa é compatível com os seguintes cenários:
    - Pasta
        - Criar pasta.
        - Atualizar descrição da pasta.
    - Project
        - Configurar o valor dos parâmetros, há suporte para o valor literal e o valor referenciado.
        - Adicionar referências de ambiente.
    - Ambiente
        - Criar ambiente.
        - Atualizar descrição do ambiente.
        - Criar ou atualizar variável de ambiente.

## <a name="ssis-build-task"></a>Tarefa Build do SSIS

![tarefa de build](media/ssis-build-task.png)

### <a name="properties"></a>Propriedades

#### <a name="project-path"></a>Caminho do projeto

Caminho da pasta do projeto ou do arquivo a ser compilado. Se um caminho de pasta for especificado, a tarefa Build do SSIS pesquisará todos os arquivos dtproj de maneira recursiva nessa pasta e os criará.

O caminho do projeto não pode estar *vazio*, definido como **.** para criar a partir da pasta raiz do repositório.

#### <a name="project-configuration"></a>Configuração do projeto

Nome da configuração de projeto a ser usada para o build. Se ele não for fornecido, usará como padrão a primeira configuração de projeto definida em cada arquivo dtproj.

#### <a name="output-path"></a>Caminho de saída

Caminho de uma pasta separada para salvar os resultados do build, que podem ser publicados como artefatos de compilação por meio da tarefa [publicar artefatos de compilação](/azure/devops/pipelines/tasks/utility/publish-build-artifacts?view=azure-devops).

### <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

- A tarefa Build do SSIS depende do Visual Studio e do Designer SSIS, que é obrigatório nos agentes de build. Portanto, para executar a tarefa Build do SSIS no pipeline, escolha **vs2017-win2016** para agentes hospedados pela Microsoft ou instale o Visual Studio e o Designer SSIS (VS2017 + SSDT2017 ou VS2019 + extensão Projetos do SSIS) em agentes auto-hospedados.

- Para criar projetos do SSIS usando componentes prontos para uso (incluindo o feature pack do SSIS para o Azure e outros componentes de terceiros), os componentes prontos para uso precisam ser instalados no computador em que o agente de pipeline está em execução.  Para o agente hospedado pela Microsoft, o usuário pode adicionar uma [tarefa Script do PowerShell](/azure/devops/pipelines/tasks/utility/powershell?view=azure-devops) ou uma [tarefa Script de Linha de Comando](/azure/devops/pipelines/tasks/utility/command-line?view=azure-devops) para baixar e instalar os componentes antes de executar a tarefa Build do SSIS. Confira abaixo o exemplo de script do PowerShell para instalar o Feature Pack do Azure: 

```powershell
wget -Uri https://download.microsoft.com/download/E/E/0/EE0CB6A0-4105-466D-A7CA-5E39FA9AB128/SsisAzureFeaturePack_2017_x86.msi -OutFile AFP.msi

start -Wait -FilePath msiexec -Args "/i AFP.msi /quiet /l* log.txt"

cat log.txt
```

- Não há suporte para o nível de proteção **EncryptSensitiveWithPassword** e **EncryptAllWithPassword** na tarefa Build do SSIS. Verifique se todos os projetos do SSIS na base de código não estão usando esses dois níveis de proteção ou se a tarefa Build do SSIS interromperá a resposta e atingirá o tempo limite durante a execução.

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

Nome do SQL Server de destino. Pode ser o nome de um SQL Server local, de um Banco de Dados SQL do Azure ou de uma Instância Gerenciada de SQL do Azure. Essa propriedade só é visível quando o tipo de destino é SSISDB.

#### <a name="destination-path"></a>Caminho de destino

Caminho da pasta de destino no qual o arquivo de origem será implantado. Por exemplo:

- /SSISDB/\<folderName\>
- \\\\\<machineName\>\\\<shareFolderName\>\\\<optionalSubfolderName\>

A tarefa Implantação do SSIS criará a pasta e a subpasta caso elas não existam.

#### <a name="authentication-type"></a>Tipo de autenticação

Tipo de autenticação para acessar o servidor de destino especificado. Essa propriedade só é visível quando o tipo de destino é SSISDB. De modo geral, os tipos de autenticação abaixo têm suporte:

- Autenticação do Windows
- Autenticação do SQL Server
- Active Directory – Senha
- Active Directory – Integrado

Porém, o suporte ao tipo de autenticação específico depende do tipo de servidor de destino e do tipo de agente. A matriz de suporte detalhado é listada na tabela abaixo.

|Tipo de servidor de destino|Agente hospedado pela Microsoft|Agente auto-hospedado|
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

Especifique se deseja continuar a implantação para projetos ou arquivos restantes quando ocorrer um erro. Se a opção for 'Não', a tarefa Implantação do SSIS será interrompida imediatamente quando ocorrer um erro.

### <a name="limitations-and-known-issues"></a>Limitações e problemas conhecidos

Atualmente, a tarefa Implantação do SSIS não dá suporte aos seguintes cenários:

- Configurar o ambiente no catálogo do SSIS.
- Implantar o ispac no Azure SQL Server ou na Instância Gerenciada do Azure SQL que só permite a MFA (autenticação multifator).
- Implantar pacotes no Repositório de Pacotes SSIS ou no MSDB.

## <a name="ssis-catalog-configuration-task"></a>Tarefa de Configuração do Catálogo do SSIS

![tarefa de configuração do catálogo](media/ssis-catalog-configuation-task.png)

### <a name="properties"></a>Propriedades

#### <a name="configuration-file-source"></a>Origem do arquivo de configuração

Origem do arquivo JSON de configuração do catálogo do SSIS. Pode ser "Caminho do arquivo" ou "Embutido".

Confira os detalhes de como [definir a configuração do JSON](#define-configuration-json):

- Confira [um exemplo de JSON de configuração embutido](#a-sample-inline-configuration-json).
- Verifique o [esquema JSON](#json-schema).

#### <a name="configuration-json-file-path"></a>Caminho do arquivo JSON de configuração

Caminho do arquivo JSON de configuração do catálogo do SSIS. Essa propriedade só é visível ao selecionar "Caminho do arquivo" como origem do arquivo de configuração.

Para usar [variáveis de pipeline](/azure/devops/pipelines/process/variables) no arquivo JSON de configuração, você precisa adicionar uma [Tarefa de Transformação de Arquivo](/azure/devops/pipelines/tasks/utility/file-transform?view=azure-devops) antes dessa tarefa para substituir valores de configuração por variáveis de pipeline. Para obter mais informações, confira [Substituição de variável JSON](/azure/devops/pipelines/tasks/transforms-variable-substitution?tabs=Classic&view=azure-devops#json-variable-substitution).

#### <a name="inline-configuration-json"></a>JSON de configuração embutido

JSON embutido de configuração do catálogo do SSIS. Essa propriedade só é visível ao selecionar "Embutido" como origem do arquivo de configuração. As variáveis de pipeline podem ser usadas diretamente.

#### <a name="roll-back-configuration-when-error-occurs"></a>Reverter configuração quando ocorrer um erro

Se a configuração feita por esse erro deve ser revertida quando um erro ocorrer.

#### <a name="target-server"></a>Servidor de destino

Nome do SQL Server de sestino. Pode ser o nome de um SQL Server local, de um Banco de Dados SQL do Azure ou de uma Instância Gerenciada de SQL do Azure.

#### <a name="authentication-type"></a>Tipo de autenticação

Tipo de autenticação para acessar o servidor de destino especificado. De modo geral, os tipos de autenticação abaixo têm suporte:

- Autenticação do Windows
- Autenticação do SQL Server
- Active Directory – Senha
- Active Directory – Integrado

Porém, o suporte ao tipo de autenticação específico depende do tipo de servidor de destino e do tipo de agente. A matriz de suporte detalhado é listada na tabela abaixo.

|Tipo de servidor de destino|Agente hospedado pela Microsoft|Agente auto-hospedado|
|---------|---------|---------|
|SQL Server local ou VM |N/D|Autenticação do Windows|
|SQL do Azure|Autenticação do SQL Server <br> Active Directory – Senha|Autenticação do SQL Server <br> Active Directory – Senha <br> Active Directory – Integrado|

#### <a name="username"></a>Nome de Usuário

Nome de usuário para acessar o SQL Server de destino. Essa propriedade é visível apenas quando o tipo de Autenticação é Autenticação do SQL Server ou Active Directory: Senha.

#### <a name="password"></a>Senha

Senha para acessar o SQL Server de destino. Essa propriedade é visível apenas quando o tipo de Autenticação é Autenticação do SQL Server ou Active Directory: Senha.

### <a name="define-configuration-json"></a>Definir JSON de configuração

O esquema JSON de configuração tem três camadas:

- catálogo
- folder
- projeto e ambiente

![esquema de configuração de catálogo](media/catalog-configuration-schema.png)

#### <a name="a-sample-inline-configuration-json"></a>Um exemplo de JSON de configuração embutido

```json
{
  "folders": [
    {
      "name": "devopsdemo",
      "description": "devops demo folder",
      "projects": [
        {
          "name": "catalog devops",
          "parameters": [
            {
              "name": "password",
              "container": "Package.dtsx",
              "value": "passwd",
              "valueType": "referenced"
            },
            {
              "name": "serverName",
              "container": "catalog devops",
              "value": "localhost",
              "valueType": "literal"
            }
          ],
          "references": [
            {
              "environmentName": "test",
              "environmentFolder": "devopsdemo"
            },
            {
              "environmentName": "test",
              "environmentFolder": "."
            }
          ]
        }
      ],
      "environments": [
        {
          "name": "test",
          "description": "test",
          "variables": [
            {
              "name": "passwd",
              "type": "string",
              "description": "",
              "value": "$(SSISDBServerAdminPassword)",
              "sensitive": true
            },
            {
              "name": "serverName",
              "type": "string",
              "description": "",
              "value": "$(TargetServerName)",
              "sensitive": false
            }
          ]
        }
      ]
    }
  ]
}
```

#### <a name="json-schema"></a>JSON schema

##### <a name="catalog-attributes"></a>Atributos do catálogo

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|pastas  |Uma matriz de objetos de pasta. Cada objeto contém informações de configuração para uma pasta de catálogo.|Confira *Atributos da pasta* para ver o esquema de um objeto de pasta.|

##### <a name="folder-attributes"></a>Atributos da pasta

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|name  |Nome da pasta do catálogo.|A pasta será criada se não existir.|
|descrição|Descrição da pasta do catálogo.|O valor de *nulo* será ignorado.|
|projects|Uma matriz de objetos do projeto. Cada objeto contém informações de configuração para um projeto.|Confira *Atributos de projeto* para ver o esquema de um objeto de projeto.|
|environments|Uma matriz de objetos de ambiente. Cada objeto contém informações de configuração para um ambiente.|Confira *Atributos de ambiente* para ver o esquema de um objeto de ambiente.|

##### <a name="project-attributes"></a>Atributos de projeto

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|name|Nome do projeto. |O objeto do projeto será ignorado se o projeto não existir na pasta pai.|
|parâmetros|Uma matriz de objetos de parâmetro. Cada objeto contém informações de configuração para um parâmetro.|Confira *Atributos do parâmetro* para ver o esquema de um objeto de parâmetro.|
|referências|Uma matriz de objetos de referência. Cada objeto representa uma referência de ambiente para o projeto de destino.|Confira *Atributos de referência* para ver um esquema de objeto de referência.|

##### <a name="parameter-attributes"></a>Atributos de parâmetro

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|name|Nome do parâmetro.|<li>O parâmetro pode ser um parâmetro de projeto ou um parâmetro de pacote. <li>O parâmetro será ignorado se ele não existir. <li>Se o parâmetro for uma propriedade do gerenciador de conexões, o nome deverá estar no formato **CM.\<Connection Manager Name>.\<Property Name>** . |
|contêiner|Contêiner do parâmetro.|<li>Se o parâmetro for um parâmetro de projeto, o *contêiner* deverá ser o nome do projeto. <li>Se for um parâmetro de pacote, o *contêiner* deverá ser o nome do pacote com a extensão **.dtsx**.|
|value|Valor do parâmetro.|<li>Quando *valueType* é *referenciado*: O valor é uma referência a uma variável de ambiente no tipo *cadeia de caracteres*. <li> Quando *valueType* é *literal*: Esse atributo dá suporte a qualquer valor JSON *booliano*, de *número* e *cadeia de caracteres* válido. <li> O valor será convertido para o tipo de parâmetro de destino. O erro ocorrerá se não for possível convertê-lo.<li> O valor de *null* é inválido. A tarefa ignorará esse objeto de parâmetro e emitir um aviso.|
|valueType|Tipo do valor do parâmetro.|Os tipos válidos são: <br> *literal*: a atributo *valor* representa um valor literal. <br> *referenciado*: o atributo *valor* representa uma referência a uma variável de ambiente.|

##### <a name="reference-attributes"></a>Atributo de referência

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|environmentFolder|O nome da pasta do ambiente.|A pasta será criada se não existir. <br> O valor pode ser ".", que representa a pasta pai do projeto, que faz referência ao ambiente.|
|environmentName|Nome do ambiente referenciado.|O ambiente especificado será criado se não existir.|

##### <a name="environment-attributes"></a>Atributos de ambiente

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|name|Nome do ambiente.|O ambiente será criado se não existir.|
|descrição|Descrição do ambiente.|O valor de *nulo* será ignorado.|
|variáveis|Uma matriz de objetos de variável.|Cada objeto contém informações de configuração para uma variável de ambiente. Confira *Atributos de variáveis* para ver o esquema de um objeto de variável.|

##### <a name="variable-attributes"></a>Atributos de variáveis

|Propriedade  |Descrição  |Observações  |
|---------|---------|---------|
|name|Nome da variável de ambiente.|A variável de ambiente será criada se não existir.|
|type|Tipo de dados da variável de ambiente.|Os tipos válidos são: <br> *booleano* <br> *byte* <br> *datetime* <br> decimal <br> *double* <br> *int16* <br> *int32* <br> *int64* <br> *sbyte* <br> *single* <br> *cadeia de caracteres* <br> *uint32* <br> *uint64*|
|descrição|Descrição da variável de ambiente.|O valor de *nulo* será ignorado.|
|value|Valor da variável de ambiente.|Esse atributo dá suporte a qualquer valor JSON booliano, de número e cadeia de caracteres válido.<br> O valor será convertido para o tipo especificado pelo atributo **type**. Ocorrerá um erro se houver falha na conversão.<br>O valor de *null* é inválido. A tarefa ignorará esse objeto de variável de ambiente e emitir um aviso.|
|sensitive|Se o valor da variável de ambiente é confidencial.|As entradas válidas são: <br> *true* <br> *false*|

## <a name="release-notes"></a>Notas de versão

### <a name="version-102"></a>Versão 1.0.2

Data de lançamento: 26 de maio de 2020

- Foi corrigido um problema em que a tarefa de Configuração do Catálogo do SSIS poderia falhar em alguns casos após a conclusão do trabalho de configuração.

### <a name="version-101"></a>Versão 1.0.1

Data de lançamento: 9 de maio de 2020

- Corrigido um problema em que a tarefa de compilação do SSIS sempre compilava toda a solução, mesmo se apenas um único arquivo dtproj estivesse especificado como o caminho do projeto.

### <a name="version-100"></a>Versão 1.0.0

Data de lançamento: 8 de maio de 2020

- Versão de GA (disponibilidade geral).
- Adicionada uma restrição da versão mínima do .NET Framework no agente. Atualmente, a versão mínima do .NET Framework é 4.6.2.
- Descrição refinada da tarefa de Build do SSIS e da tarefa de implantação do SSIS.

### <a name="version-020-preview"></a>Versão 0.2.0, versão prévia

Data de lançamento: 31 de março de 2020

- Adicionar Tarefa de Configuração do Catálogo do SSIS.

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