---
title: Extensão do PowerShell
description: Saiba como instalar e usar a extensão do PowerShell para Azure Data Studio, que fornece suporte avançado ao editor do PowerShell para escrever e depurar scripts.
ms.custom: seodec18
ms.date: 04/19/2019
ms.reviewer: alayu, maghan, sstein
ms.prod: azure-data-studio
ms.technology: azure-data-studio
ms.topic: conceptual
author: SQLvariant
ms.author: aanelson
manager: matthend
ms.openlocfilehash: c3edd5b618a6119021a69f90f4e90341ae6360bb
ms.sourcegitcommit: 7345e4f05d6c06e1bcd73747a4a47873b3f3251f
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/24/2020
ms.locfileid: "88766535"
---
# <a name="powershell-editor-support-for-azure-data-studio"></a>Suporte do Editor do PowerShell para Azure Data Studio

Essa extensão fornece suporte avançado ao editor do PowerShell no [Azure Data Studio](https://github.com/Microsoft/azuredatastudio).
Agora você pode escrever e depurar scripts do PowerShell usando a excelente interface semelhante ao IDE que o Azure Data Studio fornece.

![Extensão do PowerShell](media/powershell-extension/powershell-extension.png)

## <a name="features"></a>Recursos

- Realce de sintaxe
- Snippets de código
- IntelliSense para cmdlets e mais
- Análise baseada em regra fornecida pelo [Analisador de Script do PowerShell](http://github.com/PowerShell/PSScriptAnalyzer)
- Ir para a Definição de cmdlets e variáveis
- Localizar Referências de cmdlets e variáveis
- Descoberta de símbolo de documento e de workspace
- Executar a seleção selecionada de código do PowerShell usando <kbd>F8</kbd>
- Iniciar ajuda online para o símbolo embaixo do cursor usando <kbd>Ctrl</kbd>+<kbd>F1</kbd>
- Suporte básico ao console interativo!

## <a name="installing-the-extension"></a>Instalar a extensão

Você pode instalar a versão oficial da extensão do PowerShell seguindo as etapas na [documentação do Azure Data Studio](./extensions.md).
No painel Extensões, pesquise a extensão “PowerShell” e instale-a lá.  Você será notificado automaticamente sobre atualizações futuras de extensão!

Você também pode instalar um pacote VSIX na página nossa [página Versões](https://github.com/PowerShell/vscode-powershell/releases) instalá-lo usando a linha de comando:

```powershell
azuredatastudio --install-extension PowerShell-<version>.vsix
```

## <a name="platform-support"></a>Suporte a plataforma

- **Windows 7 até 10** com o Windows PowerShell v3 e superior e o PowerShell Core
- **Linux** com PowerShell Core (todas as distribuições com suporte do PowerShell)
- **macOS** com o PowerShell Core

Leia as [Perguntas frequentes](https://github.com/PowerShell/vscode-powershell/wiki/FAQ) para obter respostas para perguntas comuns.

## <a name="installing-powershell-core"></a>Instalar o PowerShell Core

Se você estiver executando o Azure Data Studio no macOS ou no Linux, talvez precise instalar também o PowerShell Core.

O PowerShell Core é um projeto de software livre no [GitHub](https://github.com/powershell/powershell).
Para saber mais sobre como instalar o PowerShell Core em plataformas macOS ou Linux, confira os seguintes artigos:

- [Instalar o PowerShell Core no Linux](/powershell/scripting/install/installing-powershell-core-on-linux?view=powershell-6)
- [Instalar o PowerShell Core no macOS](/powershell/scripting/install/installing-powershell-core-on-macos?view=powershell-6)

## <a name="example-scripts"></a>Scripts de exemplo

Há alguns scripts de exemplo na pasta `examples` da extensão que você pode usar para descobrir a funcionalidade de edição e de depuração do PowerShell.  Confira o arquivo [README.md](https://github.com/PowerShell/vscode-powershell/blob/master/examples/README.md) incluído para saber mais sobre como usá-los.

Essa pasta pode ser encontrada no seguinte caminho:

```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.PowerShell-<version>/examples
```

ou se você estiver usando a versão prévia da extensão

 ```powershell
$HOME/.azuredatastudio/extensions/ms-vscode.powershell-preview-<version>/examples
```

Para abrir/exibir os exemplos da extensão no Azure Data Studio, execute o seguinte código em seu prompt de comando do PowerShell:

```powershell
azuredatastudio (Get-ChildItem $Home\.azuredatastudio\extensions\ms-vscode.PowerShell-*\examples)[-1]
```

### <a name="creating-and-opening-files"></a>Criar e abrir arquivos

Para criar um arquivo e abri-lo no editor, use o New-EditorFile de dentro do Terminal Integrado do PowerShell.

```powershell
PS C:\temp> New-EditorFile ExportData.ps1
```

Esse comando funciona para qualquer tipo de arquivo, não apenas arquivos do PowerShell.

```powershell
PS C:\temp> New-EditorFile ImportData.py
```

Para abrir um ou mais arquivos no Azure Data Studio, use o comando `Open-EditorFile`.

```powershell
Open-EditorFile ExportData.ps1, ImportData.py
```

### <a name="no-focus-on-console-when-executing"></a>Sem foco no console ao executar

Para os usuários que estão acostumados a trabalhar com o SSMS, você está acostumado a poder executar uma consulta e poder executá-la novamente sem precisar voltar para o painel de consultas.  Nesse caso, o comportamento padrão do editor de código pode parecer estranho para você.  Para manter o foco no editor quando você executa com <kbd>F8</kbd>, altere a seguinte configuração:

```json
"powershell.integratedConsole.focusConsoleOnExecute": false
```

O padrão é `true` para fins de acessibilidade.

Lembre-se de que essa configuração impedirá que o foco mude para o console, mesmo quando você usar um comando que chame explicitamente chamadas para entrada, como `Get-Credential`.

## <a name="sql-powershell-examples"></a>Exemplos do SQL PowerShell
Para usar estes exemplos (abaixo), é necessário instalar o módulo SqlServer na [Galeria do PowerShell](https://www.powershellgallery.com/packages/SqlServer).

```powershell
Install-Module -Name SqlServer
```

> [!NOTE]
> Com a versão `21.1.18102` e posterior, o módulo `SqlServer` dá suporte ao [PowerShell Core](https://github.com/PowerShell/PowerShell) 6.2 e superior, além do Windows PowerShell.

Neste exemplo, usamos o cmdlet `Get-SqlInstance` para obter os objetos SMO do servidor para ServerA e ServerB.  A saída padrão desse comando incluirá o nome da instância, a versão, o Service Pack e o nível de atualização da CU das instâncias.

```powershell
Get-SqlInstance -ServerInstance ServerA, ServerB
```

Veja um exemplo de qual será a aparência da saída:

```
Instance Name             Version    ProductLevel UpdateLevel  HostPlatform HostDistribution
-------------             -------    ------------ -----------  ------------ ----------------
ServerA                   13.0.5233  SP2          CU4          Windows      Windows Server 2016 Datacenter
ServerB                   14.0.3045  RTM          CU12         Linux        Ubuntu
```
O módulo `SqlServer` contém um provedor chamado `SQLRegistration` que permite que você acesse de maneira programática os seguintes tipos de conexões salvas do SQL Server:

+ Servidor do Mecanismo de Banco de Dados (Servidores Registrados)
+ CMS (Sistema de Gerenciamento Central)
+ Serviços de análise
+ Integration Services
+ Reporting Services

 No exemplo a seguir, faremos um `dir` (alias de `Get-ChildItem`) para obter a lista de todas as instâncias do SQL Server listadas em seu arquivo de Servidores Registrados.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse 
```

Veja um exemplo de qual poderia ser a aparência da saída:

```powershell
Mode Name
---- ----
-    ServerA
-    ServerB
-    localhost\SQL2017
-    localhost\SQL2016Happy
-    localhost\SQL2017
```

Para muitas operações que envolvem um banco de dados ou objetos dentro de um banco de dados, o cmdlet `Get-SqlDatabase` pode ser usado.  Se você fornecer valores para os parâmetros `-ServerInstance` e `-Database`, somente esse objeto de banco de dados será recuperado.  No entanto, se você especificar somente o parâmetro `-ServerInstance`, uma lista completa de todos os bancos de dados nessa instância será retornada.

Veja um exemplo de qual será a aparência da saída:

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

Este próximo exemplo usa o cmdlet `Get-SqlDatabase` para recuperar uma lista de todos os bancos de dados na instância ServerB e apresenta uma grade/tabela (que usa o cmdlet `Out-GridView`) para selecionar de quais bancos de dados o backup deve ser feito.  Quando o usuário clicar no botão “OK”, apenas o backup dos bancos de dados realçados será feito.

```powershell
Get-SqlDatabase -ServerInstance ServerB |
Out-GridView -PassThru |
Backup-SqlDatabase -CompressionOption On
```

Este exemplo, novamente, obtém a lista de todas as instâncias do SQL Server listadas no arquivo de Servidores Registrados e, em seguida, chama o `Get-SqlAgentJobHistory` que relata cada trabalho com falha do SQL Agent desde a meia-noite para cada instância do SQL Server listada.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE {$_.Mode -ne 'd' } |
FOREACH {
    Get-SqlAgentJobHistory -ServerInstance  $_.Name -Since Midnight -OutcomesType Failed
}
```

Neste exemplo, faremos um `dir` (alias de `Get-ChildItem`) para obter a lista de todas as instâncias do SQL Server listadas em seu arquivo de Servidores Registrados e usaremos o cmdlet `Get-SqlDatabase` para obter uma lista de bancos de dados para cada uma dessas instâncias.

```powershell
dir 'SQLSERVER:\SQLRegistration\Database Engine Server Group' -Recurse |
WHERE { $_.Mode -ne 'd' } |
FOREACH {
    Get-SqlDatabase -ServerInstance $_.Name
}
```

Veja um exemplo de qual será a aparência da saída:

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

## <a name="reporting-problems"></a>Relatar problemas

Se você tiver problemas com a Extensão do PowerShell, confira [os documentos de solução de problemas](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md) para saber mais sobre como diagnosticar e relatar problemas.

#### <a name="security-note"></a>Observação sobre segurança

Para obter problemas de segurança, confira [aqui](https://github.com/PowerShell/vscode-powershell/blob/master/docs/troubleshooting.md#note-on-security).

## <a name="contributing-to-the-code"></a>Contribuir com o código

Confira a [documentação de desenvolvimento](https://github.com/PowerShell/vscode-powershell/blob/master/docs/development.md) para obter mais detalhes sobre como contribuir com essa extensão!

## <a name="maintainers"></a>Mantenedores

- [Keith Hill](https://github.com/rkeithhill) - [@r_keith_hill](http://twitter.com/r_keith_hill)
- Tyler Leonhardt – [@TylerLeonhardt](http://twitter.com/tylerleonhardt)
- [Rob Holt](https://github.com/rjmholt)

## <a name="license"></a>Licença

Essa extensão está [licenciada nos termos da Licença do MIT](https://github.com/PowerShell/vscode-powershell/blob/master/LICENSE.txt). Para obter detalhes sobre os binários de terceiros que incluímos com as versões deste projeto, confira o arquivo [avisos de terceiros](https://github.com/PowerShell/vscode-powershell/blob/master/Third%20Party%20Notices.txt).

## <a name="code-of-conduct"></a>Código de Conduta

Este projeto adotou o [Código de Conduta de Software Livre da Microsoft][conduct-code].
Para saber mais, confira as [Perguntas frequentes sobre o Código de Conduta][conduct-FAQ] ou contate o [opencode@microsoft.com][conduct-email] caso tenha outras dúvidas ou comentários.

[conduct-code]: https://opensource.microsoft.com/codeofconduct/
[conduct-FAQ]: https://opensource.microsoft.com/codeofconduct/faq/
[conduct-email]: mailto:opencode@microsoft.com