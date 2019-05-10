---
title: Extensão do PowerShell
titleSuffix: Azure Data Studio
description: Instalar e usar o PowerShell para o Studio de dados do Azure
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu; sstein
ms.prod: sql
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: c7a2dbdccf92a52d5733a04915acc3f76dc3f033
ms.sourcegitcommit: bb5484b08f2aed3319a7c9f6b32d26cff5591dae
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/06/2019
ms.locfileid: "65105957"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Suporte ao Editor do PowerShell para o Studio de dados do Azure

Essa extensão oferece suporte avançado de editor do PowerShell no [Studio do Azure Data](https://github.com/Microsoft/azuredatastudio).
Agora você pode escrever e depurar scripts do PowerShell usando o excelente IDE interface que fornece Studio de dados do Azure.

![Extensão do PowerShell](media/powershell-extension/powershell-extension.png)


## <a name="features"></a>Recursos

- Realce de sintaxe
- Snippets de código
- IntelliSense para cmdlets e muito mais
- Análise com base em regra fornecida pelo [PowerShell Script Analyzer](http://github.com/PowerShell/PSScriptAnalyzer)
- Ir para definição de cmdlets e variáveis
- Localizar referências de cmdlets e variáveis
- Descoberta de símbolo do documento e o espaço de trabalho
- Executar seleção selecionada do código do PowerShell usando <kbd>F8</kbd>
- Iniciar a Ajuda online para o símbolo sob o cursor usando <kbd>Ctrl</kbd>+<kbd>F1</kbd>
- Suporte básico de console interativo!


## <a name="installing-the-extension"></a>Instalando a extensão

Você pode instalar a versão oficial da extensão do PowerShell seguindo as etapas a [documentação do Azure Data Studio](https://docs.microsoft.com/sql/azure-data-studio/extensions).
No painel extensões, pesquise a extensão do "PowerShell" e instalá-lo lá.  Você será notificado automaticamente sobre todas as atualizações de extensão futura!

Você também pode instalar um pacote VSIX do nosso [página de versões](https://github.com/PowerShell/vscode-powershell/releases) e instalá-lo por meio da linha de comando:

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>Suporte de plataforma

- **Windows 7 a 10** com o Windows PowerShell v3 e superior e o PowerShell Core
- **Linux** com o PowerShell Core (todas as distribuições com suporte do PowerShell)
- **macOS** com o PowerShell Core

Leia as [perguntas frequentes sobre](https://github.com/PowerShell/vscode-powershell/wiki/FAQ) para obter respostas a perguntas comuns.

## <a name="installing-powershell-core"></a>Instalar o PowerShell Core

Se você estiver executando o estúdio de dados do Azure no MacOS ou Linux, você também precisará instalar o PowerShell Core.

O PowerShell Core é um projeto de código-fonte aberto no [GitHub](https://github.com/powershell/powershell).
Para obter mais informações sobre como instalar o PowerShell Core nas plataformas MacOS ou Linux, consulte os seguintes artigos:

- [Instalar o PowerShell Core no Linux](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalar o PowerShell Core no macOS](https://docs.microsoft.com/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>Scripts de exemplo

Há alguns scripts de exemplo na extensão do `examples` pasta que você pode usar para descobrir o PowerShell, edição e depuração de funcionalidade.  Confira os incluídos [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) arquivo para saber mais sobre como usá-los.

Essa pasta pode ser encontrada no seguinte caminho:

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

ou, se você estiver usando a versão prévia da extensão

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Para abrir/exibir exemplos de extensão no estúdio de dados do Azure, execute o seguinte código em seu prompt de comando do PowerShell:

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>Criando e abrindo arquivos

Para criar e abrir um novo arquivo dentro do editor, use o New-EditorFile de dentro do Terminal integrado do PowerShell.

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

Esse comando funciona para qualquer tipo de arquivo, não apenas arquivos do PowerShell.

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

Para abrir um ou mais arquivos no estúdio de dados do Azure, use o `Open-EditorFile` comando.

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>Sem foco no console ao executar

Para os usuários que são usados para trabalhar com o SSMS, você está acostumado para ser capaz de executar uma consulta e, em seguida, ser capaz de executá-la novamente novamente sem a necessidade de voltar para o painel de consulta.  Nesse caso, o comportamento padrão do editor de código pode parecer estranho para você.  Para manter o foco no editor quando você executa com <kbd>F8</kbd> altere a seguinte configuração:

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

O padrão é `true` para fins de acessibilidade.

Lembre-se de que essa configuração impedirá que o foco mesmo quando você usa um comando que explicitamente chamadas de entrada, como a alteração para o console, `Get-Credential`.

## <a name="sql-powershell-examples"></a>Exemplos de PowerShell do SQL
Para usar esses exemplos (abaixo), você precisa instalar o módulo do SqlServer do [da Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> Com a versão `21.1.18102` e superior, o `SqlServer` módulo oferece suporte a [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 e para cima, além do Windows PowerShell.

Neste exemplo, usamos o `Get-SqlInstance` para obter os objetos de servidor SMO para ServerA e ServerB.  O padrão de saída para esse comando incluirá o nome da instância, versão, Service Pack & nível de atualização CU das instâncias.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Aqui está um exemplo que saída terá a seguinte aparência:

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
O `SqlServer` módulo contém um provedor chamado `SQLRegistration` que permite acessar programaticamente os tipos seguintes de conexões do SQL Server salvas:

+ Servidor do mecanismo de banco de dados (servidores registrados)
+ Servidor de gerenciamento central (CMS)
+ Analysis Services
+ Integration Services
+ Reporting Services

 No exemplo a seguir, faremos uma `dir` (alias para `Get-ChildItem`) para obter a lista de todas as instâncias do SQL Server listados no arquivo de servidores registrados.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

Aqui está um exemplo que a saída pode ser semelhante:

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

Para muitas operações que envolvem um banco de dados ou objetos dentro de um banco de dados, o `Get-SqlDatabase` cmdlet pode ser usado.  Se você fornecer valores para a ambos os `-ServerInstance` e `-Database` parâmetros, apenas esse objeto de um banco de dados serão recuperados.  No entanto, se você especificar apenas o `-ServerInstance` parâmetro, uma lista completa de todos os bancos de dados nessa instância será retornada.

Aqui está um exemplo que saída terá a seguinte aparência:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa
master               Normal        6.00 MB  368.00 KB Simple       140 sa
model                Normal       16.00 MB    5.53 MB Full         140 sa
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa
```

O exemplo a seguir usa o `Get-SqlDatabase` cmdlet para recuperar uma lista de todos os bancos de dados na instância do servidor b, em seguida, apresenta uma grade/tabela (usando o `Out-GridView` cmdlet) para selecionar quais bancos de dados devem ser feitos backup.  Depois que o usuário clica no botão "Okey", somente os bancos de dados realçados serão submetidos a backup.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

Neste exemplo, novamente, obtém a lista de todas as instâncias do SQL Server listados no arquivo de servidores registrados, em seguida, chama o `Get-SqlAgentJobHistory` que relata cada trabalho do SQL Agent com falha desde a meia-noite, cada instância do SQL Server listada.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

Neste exemplo, vamos fazer uma `dir` (alias para `Get-ChildItem`) para obter a lista de todas as instâncias do SQL Server listados no arquivo de servidores registrados e, em seguida, use o `Get-SqlDatabase` para obter uma lista de bancos de dados para cada uma dessas instâncias.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Aqui está um exemplo que saída terá a seguinte aparência:

```
Name                 Status           Size     Space  Recovery Compat. Owner
                                            Available  Model     Level      
----                 ------           ---- ---------- -------- ------- -----
AdventureWorks2017   Normal      336.00 MB   57.01 MB Simple       140 sa   
master               Normal        6.00 MB  368.00 KB Simple       140 sa   
model                Normal       16.00 MB    5.53 MB Full         140 sa   
msdb                 Normal       48.44 MB    1.70 MB Simple       140 sa   
PBIRS                Normal      144.00 MB   55.95 MB Full         140 sa   
PBIRSTempDB          Normal       16.00 MB    4.20 MB Simple       140 sa   
SSISDB               Normal      325.06 MB   26.21 MB Full         140 sa   
tempdb               Normal       72.00 MB   61.25 MB Simple       140 sa   
WideWorldImporters   Normal         3.2 GB     2.6 GB Simple       130 sa   
```

## <a name="reporting-problems"></a>Problemas de relatórios

Se você tiver problemas com a extensão do PowerShell, consulte [os documentos de solução de problemas](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md) para obter informações sobre como diagnosticar e relatar problemas.

#### <a name="security-note"></a>Observação sobre segurança

Para quaisquer problemas de segurança, consulte [aqui](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security).

## <a name="contributing-to-the-code"></a>Contribuindo para o código

Confira a [documentação de desenvolvimento](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md) para obter mais detalhes sobre como Contribuir para essa extensão!

## <a name="maintainers"></a>Mantenedores

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- [Tyler Leonhardt](https://github.com/tylerl0706) - [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>Licença

Essa extensão é [licenciado sob a licença MIT](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt). Para obter detalhes sobre os binários de terceiros que são incluídos com as versões desse projeto, consulte a [avisos de terceiros](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt) arquivo.

## <a name="code-of-conductconduct-md"></a>[Código de conduta][conduct-md]

Este projeto adotou o [Microsoft código de conduta de software livre][conduct-code].
Para obter mais informações, consulte o [código de conduta perguntas Frequentes] [ conduct-FAQ] ou entre em contato com [ opencode@microsoft.com ] [ conduct-email] com quaisquer outras perguntas ou comentários.

[conduct-code]: http://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: http://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com
[conduct-md]: https://github.com/PowerShell/vscode-powershell/blob/master/CODE_OF_CONDUCT.md
