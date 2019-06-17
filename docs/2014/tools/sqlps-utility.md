---
title: Utilitário sqlps | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: tools-other
ms.topic: conceptual
helpviewer_keywords:
- sqlps utility
- PowerShell [SQL Server], sqlps utility
ms.assetid: 4b2515a6-12c3-44fb-b263-1c567681cd2b
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: b25921a7b48ecd818527dd95ebc2d8714cb6871d
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "63187075"
---
# <a name="sqlps-utility"></a>Utilitário sqlps
  O utilitário `sqlps` inicia uma sessão do Windows PowerShell 2.0 com os cmdlets e o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell carregados e registrados. Você pode inserir comandos ou scripts do PowerShell que usam os componentes do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell para trabalhar com instâncias do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e seus objetos.  
  
> [!IMPORTANT]  
>  [!INCLUDE[ssNoteDepFutureAvoid](../includes/ssnotedepfutureavoid-md.md)] Use o módulo `sqlps` do PowerShell. Para obter mais informações sobre o `sqlps` módulo, consulte [importar o módulo SQLPS](../database-engine/import-the-sqlps-module.md).  
  
## <a name="syntax"></a>Sintaxe  
  
```  
  
      sqlps   
[ [ [ -NoLogo ][ -NoExit ][ -NoProfile ]  
    [ -OutPutFormat { Text | XML } ] [ -InPutFormat { Text | XML } ]  
  ]  
  [ -Command { -  
             | script_block [ -argsargument_array ]  
             | string [ command_parameters ]  
             }  
  ]  
]  
[ -? | -Help ]  
```  
  
## <a name="arguments"></a>Argumentos  
 **-NoLogo**  
 Especifica que o utilitário `sqlps` oculta a faixa de direitos autorais quando é iniciado.  
  
 **-NoExit**  
 Especifica que o utilitário `sqlps` continua em execução após a conclusão dos comandos de inicialização.  
  
 **-NoProfile**  
 Especifica que o utilitário `sqlps` não carrega um perfil de usuário. Os perfis de usuário registram alias, funções e variáveis usados com frequência para uso em sessões do PowerShell.  
  
 **-OutPutFormat** { **Text** | **XML** }  
 Especifica que o `sqlps` utilitário saída formatada como texto cadeias de caracteres (**texto**) ou em um formato CLIXML serializado (**XML**).  
  
 **-InPutFormat** { **Text** | **XML** }  
 Especifica que a entrada para o `sqlps` utilitário é formatado como cadeias de caracteres de texto (**texto**) ou em um formato CLIXML serializado (**XML**).  
  
 **-Command**  
 Especifica o comando para a execução do utilitário `sqlps`. O `sqlps` utilitário executa o comando e fecha em seguida, a menos que **- NoExit** também for especificado. Não especifique outras opções depois de **-Command**, pois elas serão lidas como parâmetros de comando.  
  
 **-**  
 **-Comando -** Especifica que o `sqlps` utilitário lê a entrada a partir da entrada padrão.  
  
 *script_block* [ **-args**_argument_array_ ]  
 Especifica um bloco de comandos de PowerShell para executar. O bloco deve ficar entre chaves: {}. *Script_block* só pode ser especificado quando o `sqlps` utilitário é chamado do **PowerShell** ou outro `sqlps` sessão do utilitário. O *argument_array* é uma matriz de variáveis do PowerShell que contêm os argumentos para os comandos do PowerShell em *script_block*.  
  
 *string* [ *command_parameters* ]  
 Especifica que uma cadeia de caracteres contendo os comandos do PowerShell seja executada. Use o formato **"& { *`command`* }"** . As aspas indicam uma cadeia de caracteres e o invoke operador (&) faz com que o `sqlps` utilitário para executar o comando.  
  
 [ **-?** |  **-Help** ]  
 Mostra o resumo da sintaxe de opções do utilitário `sqlps`.  
  
## <a name="remarks"></a>Comentários  
 O `sqlps` utilitário inicia o ambiente do PowerShell (PowerShell.exe) e carrega o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] módulo do PowerShell. O módulo, também chamado `sqlps`, carrega e registra esses [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] snap-ins do PowerShell:  
  
-   Microsoft.SqlServer.Management.PSProvider.dll  
  
     Implementa o provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] PowerShell e os cmdlets associados, como **Encode-SqlName** e **Decode-SqlName**.  
  
-   Microsoft.SqlServer.Management.PSSnapin.dll  
  
     Implementa os cmdlets **Invoke-Sqlcmd** e **Invoke-PolicyEvaluation** .  
  
 É possível usar o utilitário `sqlps` para fazer o seguinte:  
  
-   Executar comandos do PowerShell de forma interativa.  
  
-   Executar arquivos de script do PowerShell.  
  
-   Executar cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar os caminhos de provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar pela hierarquia dos objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
 Por padrão, o `sqlps` utilitário é executado com a política de execução de scripts definida como **Restricted**. Isso impede a execução de quaisquer scripts do PowerShell. Você pode usar o cmdlet **Set-ExecutionPolicy** a fim de habilitar a execução de scripts assinados ou de qualquer script. Execute apenas scripts de fontes confiáveis e proteja todos os arquivos de entrada e saída usando as permissões NTFS adequadas. Para obter mais informações sobre como habilitar scripts do PowerShell, consulte [Running Windows PowerShell Scripts](https://www.tech-recipes.com/rx/2513/powershell_enable_script_support/)(a página pode estar em inglês).  
  
 A versão do utilitário `sqlps` no [!INCLUDE[ssKatmai](../includes/sskatmai-md.md)] e no [!INCLUDE[ssKilimanjaro](../includes/sskilimanjaro-md.md)] foi implementada como um minishell do Windows PowerShell 1.0. Os minishells têm determinadas restrições, como não permitir que os usuários carreguem snap-ins diferentes dos carregados pelo minishell. Essas restrições não se aplicam à versão [!INCLUDE[ssSQL11](../includes/sssql11-md.md)] e superiores do utilitário, que foi alterado para usar o módulo `sqlps`.  
  
## <a name="examples"></a>Exemplos  
 **A. Executar o utilitário sqlps no modo interativo padrão, sem a faixa de direitos autorais**  
  
```  
sqlps -NoLogo  
```  
  
 **B. Executar um script do SQL Server PowerShell no prompt de comando**  
  
```  
sqlps -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
 **C. Executar um script do SQL Server PowerShell usando o prompt de comando e manter a execução após a conclusão do script**  
  
```  
sqlps -NoExit -Command "&{.\MyFolder.MyScript.ps1}"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Habilitar ou desabilitar um protocolo de rede de servidor](../database-engine/configure-windows/enable-or-disable-a-server-network-protocol.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
