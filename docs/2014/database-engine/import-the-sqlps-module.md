---
title: Importar o módulo SQLPS | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: e687fd8c7fcd7c21f8aac9b546492a8f9bd4a644
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48077228"
---
# <a name="import-the-sqlps-module"></a>Importar o módulo SQLPS
  A maneira recomendada para gerenciar o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] no PowerShell é importar o módulo `sqlps` para um ambiente do Windows PowerShell 2.0. O módulo carrega e registra os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e assemblies de capacidade de gerenciamento.  
  
1.  **Antes de começar:**  [Segurança](#Security)  
  
2.  **Para carregar o módulo:**  [Carregar o módulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Depois de importar o módulo `sqlps` no Windows PowerShell, você poderá:  
  
-   Executar comandos do Windows PowerShell de forma interativa.  
  
-   Executar arquivos de script do Windows PowerShell.  
  
-   Executar cmdlets do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar os caminhos de provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] para navegar pela hierarquia dos objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
-   Usar os modelos de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] (como Microsoft.SqlServer.Management.Smo) para gerenciar objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Os verbos usados nos nomes de dois cmdlets de SQL Server (`Encode-Sqlname` e `Decode-Sqlname`) não correspondem aos verbos aprovados para o Windows PowerShell 2.0. Isso não tem nenhum efeito na sua operação, mas o Windows PowerShell gera um aviso quando o `sqlps` módulo é importado para uma sessão.  
  
###  <a name="Security"></a> Segurança  
 Por padrão, o Windows PowerShell é executado em conjunto com a política de execução de scripts definida como **Restrita**, que evita a execução de qualquer script do Windows PowerShell. Para carregar o módulo `sqlps` module, você pode usar o cmdlet `Set-ExecutionPolicy` a fim de habilitar a execução de scripts assinados ou de quaisquer outros scripts. Somente os scripts de origem confiável devem ser executados, e é preciso verificar se todos os arquivos de entrada e de saída estão usando as permissões NTFS adequadas. Para obter mais informações sobre como habilitar scripts do Windows PowerShell, consulte [Executando scripts do Windows PowerShell](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx).  
  
##  <a name="LoadSqlps"></a> Carregar o módulo sqlps  
 **Para carregar o módulo sqlps no Windows PowerShell**  
  
1.  Use o `Set-ExecutionPolicy` cmdlet para definir a política de execução do script apropriado.  
  
2.  Use o `Import-Module` cmdlet para importar o módulo sqlps. Especifique o `DisableNameChecking` parâmetro, se você desejar suprimir o aviso sobre `Encode-Sqlname` e `Decode-Sqlname`.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 Este exemplo carrega o módulo `sqlps` com verificação de nome desligado.  
  
```  
## Import the SQL Server Module.  
  
Import-Module “sqlps” -DisableNameChecking  
  
```  
  

  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)   
 [SQL Server PowerShell Provider](../powershell/sql-server-powershell-provider.md)   
 [Usar cmdlets do Mecanismo de Banco de Dados](../../2014/database-engine/use-the-database-engine-cmdlets.md)  
  
  
