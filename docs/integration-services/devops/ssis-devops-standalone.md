---
title: Ferramentas autônomas de DevOps do SSIS (SQL Server Integration Services) | Microsoft Docs
description: Saiba como criar a CI/CD do SSIS com as Ferramentas autônomas de DevOps do SSIS.
ms.date: 10/16/2020
ms.topic: conceptual
ms.prod: sql
ms.prod_service: integration-services
ms.custom: ''
ms.technology: integration-services
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 1d0e6b5fe9303269f5941ba11d231e1ca18def11
ms.sourcegitcommit: 9774e2cb8c07d4f6027fa3a5bb2852e4396b3f68
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/15/2020
ms.locfileid: "92098803"
---
# <a name="standalone-sql-server-integration-service-ssis-devops-tools-preview"></a>Ferramentas autônomas de DevOps do SSIS (SQL Server Integration Services) (versão prévia)

As **Ferramentas autônomas de DevOps do SSIS** fornecem um conjunto de executáveis para realizar tarefas de CI/CD do SSIS. Sem a dependência da instalação do Visual Studio ou do runtime do SSIS, esses executáveis podem ser facilmente integrados a qualquer plataforma de CI/CD. Os executáveis fornecidos são:

- SSISBuild.exe: crie projetos do SSIS nos modelos de implantação de projeto ou de pacote.
- SSISDeploy.exe: implante arquivos ISPAC no catálogo do SSIS ou arquivos DTSX e suas dependências no sistema de arquivos.

## <a name="installation"></a>Instalação

É necessário o .NET Framework 4.6.2 ou posterior.

Baixe o instalador mais recente no [centro de download](https://aka.ms/AA9xp65) e instale por meio do assistente ou de linha de comando:

- Instalar por meio de assistente

Clique duas vezes no arquivo .exe para instalar e especifique uma pasta para extrair os arquivos executáveis e de dependência.

![Local de instalação](media/installation-location.png)

- Instalar por meio de linha de comando

```
SSISDevOpsTools.exe /Q /C /T:<full path>
```

![Linha de comando da instalação](media/installation-command-line.png)


## <a name="ssisbuildexe"></a>SSISBuild.exe

**Sintaxe**

```
SSISBuild.exe -project|-p:<dtproj file path> [-configuration|-c:<configuration name>] [-projectPassword|-pp:<project password>] [-stripSensitive|-ss] [-output|-o:<output path>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**Parâmetros**

|Parâmetro|Descrição|
|---------|---------|
|-project \|-p:\<dtproj file path>|Caminho do arquivo dtproj a ser compilado.|
|-configuration\|-c:\<configuration name>|Nome da configuração de projeto a ser usada para o build. Se ele não for fornecido, usará como padrão a primeira configuração de projeto definida no arquivo dtproj.|
|-projectPassword\|-pp:\<project password>|Senha do projeto do SSIS e seus pacotes. Esse argumento só é válido quando o nível de proteção do projeto e dos pacotes do SSIS é EncryptSensitiveWithPassword ou EncryptAllWithPassword. Para o modelo de implantação de pacote, todos os pacotes devem compartilhar a mesma senha especificada por esse argumento.|
|-stripSensitive\|-ss|Converte o nível de proteção do projeto do SSIS para DontSaveSensitve. Quando o nível de proteção é EncryptSensitiveWithPassword ou EncryptAllWithPassword, o argumento -projectPassword deve estar definido corretamente. Essa opção só é válida para o modelo de implantação de projeto.|
|-output\|-o:\<output path>|Caminho de saída do artefato de compilação. O valor desse argumento substituirá o caminho de saída padrão na configuração do projeto.|
|-log\|-l:\<log level>[;\<log path>]|Configurações relacionadas ao log. <li>nível de log: somente os logs com nível de registros em log igual ou superior serão gravados no arquivo de log. Há quatro níveis de registros em log (de baixo a alto): DIAG, INFO, WRN, ERR. O nível de registros em log padrão será INFO se não estiver especificado. <li> caminho do log: caminho do arquivo para manter os logs. O arquivo de log não será gerado se o caminho não for especificado.|
|-quiet\|-q|Não exibe nenhum log para a saída padrão.|
|-help\|-h\|-?|Mostra informações detalhadas de uso deste utilitário de linha de comando.|

**Exemplos**

- Compile um dtproj com a primeira configuração de projeto definida, sem criptografar com senha:    
    ```
    SSISBuild.exe -p:"C:\projects\demo\demo.dtproj"
    ```

- Compile um dtproj com a configuração "DevConfiguration", criptografado com senha, e gere os artefatos de compilação em uma pasta específica:
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -o:D:\folder
    ```

- Compile um dtproj com a configuração "DevConfiguration", criptografado com senha, distribuindo seus dados confidenciais e com nível de log DIAG:
    ```
    SSISBuild.exe -p:C:\projects\demo\demo.dtproj -c:DevConfiguration -pp:encryptionpassword -ss -l:diag
    ```

## <a name="ssisdeployexe"></a>SSISDeploy.exe

**Sintaxe**

```
SSISDeploy.exe -source|-s:<source path> -destination|-d:<type>;<path>[;server] [-authType|-at:<auth type name>] [-connectionStringSuffix|-css:<connection string suffix>] [-projectPassword|-pp:<project password>] [-username|-u:<username>] [-password|-p:<password>] [-log|-l:<log level>[;<log path>]] [-quiet|-q] [-help|-h|-?]
```

**Parâmetros**

|Parâmetro|Descrição|
|---------|---------|
|-source\|-s:\<source path>|Caminho de arquivo local dos artefatos a serem implantados. ISPAC, DTSX, o caminho de pasta para DTSX e SSISDeploymentManfiest são permitidos.|
|-destination\|-d:\<type>;\<path>[;server]|Tipo de destino, caminho da pasta de destino e nome do servidor do catálogo do SSIS no qual o arquivo de origem será implantado. Atualmente, damos suporte a estes dois tipos de destino: <li> *CATALOG*: implante um ou vários arquivos ISPAC no catálogo especificado do SSIS. O caminho do destino CATALOG deve estar neste formato: <br> /SSISDB/\<folder name>[/\<project name>] <br> O <project name> opcional só é válido quando a origem especifica um único caminho de arquivo ISPAC. O nome do servidor deve ser especificado para o destino CATALOG. <li> *FILE*: implante pacotes ou arquivos especificados do SSIS em um ou vários arquivos SSISDeploymentManifest no caminho determinado do sistema de arquivos. O caminho do destino FILE pode ser um caminho de pasta local ou de rede neste formato: <br>\\\\\<machine name>\\\<folder name>[\\\<sub folder name>\...]|
|-authType\|-at:\<auth type name>|Tipo de autenticação para acessar o SQL Server. Obrigatório para o destino CATALOG. Os seguintes tipos têm suporte: <li> WIN:  Autenticação do Windows <li> SQL:  Autenticação do SQL Server <li> ADPWD:  Active Directory – Senha <li> ADINT:  Active Directory – Integrado|
|-connectionStringSuffix\|-css:\<connection string suffix> |Sufixo da cadeia de conexão usado para se conectar ao catálogo do SSIS.|
|-projectPassword\|-pp:\<project password> |Senha para descriptografar os arquivos ISPAC ou DTSX.|
|-username\|-u:\<username>  |Nome de usuário para acessar o sistema de arquivos ou catálogo especificados do SSIS. O prefixo com o nome de domínio é permitido para acesso ao sistema de arquivos.|
|-password\|-p:\<password>  |Senha para acessar o sistema de arquivos ou catálogo especificados do SSIS.|
|-log\|-l:\<log level>[;\<log path>] |Configurações relacionadas ao log para executar este utilitário. <li> nível de log: somente os logs com nível de registros em log igual ou superior serão gravados no arquivo de log. Há quatro níveis de registros em log (de baixo a alto): DIAG, INFO, WRN, ERR. O nível de registros em log padrão será INFO se não estiver especificado. <li> caminho do log: caminho do arquivo para manter os logs. O arquivo de log não será gerado se o caminho não for especificado.|
|-quiet\|-q |Não exibe nenhum log para a saída padrão.|
|-help\|-h\|-?  |Mostra informações detalhadas de uso deste utilitário de linha de comando.|

**Exemplos**

- Implante um único ISPAC não criptografado com senha no catálogo do SSIS com a autenticação do Windows.
    ```
    SSISDeploy.exe -s:D:\myfolder\demo.ispac -d:catalog;/SSISDB/destfolder;myssisserver -at:win
    ```

- Implante um único ISPAC criptografado com senha no catálogo do SSIS com a autenticação do SQL e renomeie o projeto.
    ```
    SSISDeploy.exe -s:D:\myfolder\test.ispac -d:catalog;/SSISDB/folder/testproj;myssisserver -at:sql -u:sqlusername -p:sqlpassword -pp:encryptionpassword
    ```

- Implante um único SSISDeploymentManifest e seus arquivos associados no compartilhamento de arquivos do Azure.
    ```
    SSISDeploy.exe -s:D:\myfolder\mypackage.SSISDeploymentManifest -d:file;\\myssisshare.file.core.windows.net\destfolder -u:Azure\myssisshare -p:storagekey
    ```

- Implante uma pasta de arquivos DTSX no sistema de arquivos local.
    ```
    SSISDeploy.exe -s:D:\myfolder -d:file;\\myssisshare\destfolder
    ```

## <a name="release-notes"></a>Notas de versão

### <a name="version-010-preview"></a>Versão 0.1.0 Versão prévia

Data de lançamento: 16 de outubro de 2020

Versão prévia inicial das Ferramentas autônomas de DevOps do SSIS.

## <a name="next-steps"></a>Próximas etapas

- Obtenha as [Ferramentas autônomas de DevOps do SSIS](https://aka.ms/AA9xp65)
- Caso tenha dúvidas, visite as [Perguntas e Respostas](https://marketplace.visualstudio.com/items?itemName=SSIS.ssis-devops-tools&ssr=false#qna)
