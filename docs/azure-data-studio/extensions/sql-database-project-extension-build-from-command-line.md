---
title: Compilar um projeto por meio da linha de comando
description: Compilar Projetos de Banco de Dados do SQL Server por meio da linha de comando
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: dzsquared
ms.author: drskwier
ms.reviewer: maghan, sstein
ms.custom: ''
ms.date: 08/07/2020
ms.openlocfilehash: 8c3dc88f13b7cfade3b650dcf621132d6bc22f9a
ms.sourcegitcommit: cc23d8646041336d119b74bf239a6ac305ff3d31
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/23/2020
ms.locfileid: "91123010"
---
# <a name="build-a-database-project-from-command-line"></a>Compilar um projeto de banco de dados por meio da linha de comando

Embora a extensão de Projeto de Banco de Dados do SQL para o Azure Data Studio forneça uma interface gráfica do usuário para [compilar um projeto de banco de dados](sql-database-project-extension-build.md), uma experiência de build de linha de comando também está disponível para ambientes Windows, macOS e Linux. Este artigo descreve os pré-requisitos e a sintaxe necessários para criar um projeto do SQL para dacpac por meio da linha de comando.

## <a name="prerequisites"></a>Pré-requisitos

1. Instale e configure a [extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension.md).

2. Os dlls do .NET Core a seguir e o arquivo de destino `Microsoft.Data.Tools.Schema.SqlTasts.targets` são necessários para compilar um projeto de banco de dados SQL por meio de linha de comando em todas as plataformas que dão suporte à extensão do Azure Data Studio para Projetos de Banco de Dados do SQL. Esses arquivos são criados pela extensão durante o primeiro build concluído na interface do Azure Data Studio e colocados na pasta da extensão em `BuildDirectory`.  Por exemplo, no Linux, esses arquivos são colocados em `~\.azuredatastudio\extensions\microsoft.sql-database-projects-x.x.x\BuildDirectory\`.  Copie esses 10 arquivos em uma pasta nova e acessível ou anote a localização deles.  Esse local será chamado de `DotNet Core build folder` neste documento.

    - Microsoft.Data.Tools.Schema.Sql.dll
    - Microsoft.Data.Tools.Schema.Tasks.Sql.dll
    - Microsoft.Data.Tools.Utilities.dll
    - Microsoft.SqlServer.Dac.dll
    - Microsoft.SqlServer.Dac.Extensions.dll
    - Microsoft.SqlServer.TransactSql.ScriptDom.dll
    - Microsoft.SqlServer.Types.dll
    - Microsoft.Data.Tools.Schema.SqlTasks.targets
    - System.ComponentModel.Composition.dll
    - Microsoft.Data.SqlClient.dll

3. Se o projeto foi criado no Azure Data Studio, vá diretamente para [Compilar projeto por meio da linha de comando](#build-the-project-from-the-command-line). Se o projeto foi criado no SSDT (SQL Server Data Tools), abra o projeto na extensão de Projeto de Banco de Dados do SQL do Azure Data Studio.  Abrir o projeto no Azure Data Studio atualiza automaticamente o arquivo `sqlproj` com três edições, apresentadas abaixo para seu conhecimento:

    1. Condições de importação

    ```console
    <Import Condition="'$(NetCoreBuild)' == 'true'" Project="$(NETCoreTargetsPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/> 
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' != ''" Project="$(SQLDBExtensionsRefPath)\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    <Import Condition="'$(NetCoreBuild)' != 'true' AND '$(SQLDBExtensionsRefPath)' == ''" Project="$(MSBuildExtensionsPath)\Microsoft\VisualStudio\v$(VisualStudioVersion)\SSDT\Microsoft.Data.Tools.Schema.SqlTasks.targets"/>
    ```

    2. Referência do pacote

    ```console
    <ItemGroup>
        <PackageReference Condition="'$(NetCoreBuild)' == 'true'" Include="Microsoft.NETFramework.ReferenceAssemblies" Version="1.0.0" PrivateAssets="All"/>
    </ItemGroup>
    ```

    3. Destino limpo, necessário para dar suporte à edição dupla no SSDT (SQL Server Data Tools) e no Azure Data Studio

        ```console
        <Target Name="AfterClean">
            <Delete Files="$(BaseIntermediateOutputPath)\project.assets.json"/>
        </Target>
        ```

## <a name="build-the-project-from-the-command-line"></a>Compilar projeto por meio da linha de comando

Na pasta completa do .NET, use o seguinte comando:

```console
dotnet build "<sqlproj file path>" /p:NetCoreBuild=true /p:NETCoreTargetsPath="<DotNet Core build folder>"
```

Por exemplo, em `/usr/share/dotnet` no Linux:

```console
dotnet build "/home/myuser/Documents/DatabaseProject1/DatabaseProject1.sqlproj" /p:NetCoreBuild=true /p:NETCoreTargetsPath="/home/myuser/.azuredatastudio-insiders/extensions/microsoft.sql-database-projects-0.1.2/BuildDirectory"  
```

## <a name="next-steps"></a>Próximas etapas

- [Extensão de Projetos de Banco de Dados SQL para Azure Data Studio](sql-database-project-extension.md)
- [Publicar projetos de banco de dados do SQL](sql-database-project-extension-build.md#publish-a-database-project)
