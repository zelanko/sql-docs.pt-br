---
title: "Importar o módulo SQLPS | Microsoft Docs"
ms.custom: 
ms.date: 08/01/2016
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: a972c56e-b2af-4fe6-abbd-817406e2c93a
caps.latest.revision: "12"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Active
ms.openlocfilehash: ae5fb5957e23a6ad4488a33587d227219855d6b8
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="import-the-sqlps-module"></a>Importar o módulo SQLPS
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] A maneira recomendada para gerenciar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no PowerShell é importar o módulo **sqlps** para um ambiente do Windows PowerShell. O módulo carrega e registra os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e assemblies de capacidade de gerenciamento.  A partir do Windows PowerShell 3.0, os módulos são importados automaticamente quando qualquer cmdlet ou função do módulo é usada em um comando. Esse recurso funciona em qualquer módulo em um diretório incluído no valor da variável de ambiente PSModulePath.  Para obter mais informações, consulte [Importing a PowerShell Module](https://msdn.microsoft.com/library/dd878284(v=vs.85).aspx)(Importando um módulo do PowerShell)
  
1.  **Antes de começar:**  [Segurança](#Security)  
  
2.  **Para carregar o módulo:**  [Carregar o módulo sqlps](#LoadSqlps)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Depois de importar o módulo **sqlps** no Windows PowerShell, você poderá:  
  
-   Executar comandos do Windows PowerShell de forma interativa.  
  
-   Executar arquivos de script do Windows PowerShell.  
  
-   Executar cmdlets do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usar os caminhos de provedor do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para navegar pela hierarquia dos objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Usar os modelos de objeto de gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (como Microsoft.SqlServer.Management.Smo) para gerenciar objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
> [!NOTE]  
>  Os verbos usados nos nomes de dois cmdlets de SQL Server (**Encode-Sqlname** e **Decode-Sqlname**) não correspondem aos verbos aprovados para o Windows PowerShell. Isso não tem efeito na sua operação, mas o Windows PowerShell gera um aviso quando o módulo **sqlps** é importado para uma sessão.  
  
###  <a name="Security"></a> Segurança  
 Por padrão, o Windows PowerShell é executado em conjunto com a política de execução de scripts definida como **Restrita**, que evita a execução de qualquer script do Windows PowerShell. Para carregar o módulo **sqlps** , use o cmdlet **Set-ExecutionPolicy** para habilitar a execução de scripts assinados ou de qualquer script. Somente os scripts de origem confiável devem ser executados, e é preciso verificar se todos os arquivos de entrada e de saída estão usando as permissões NTFS adequadas. Para obter mais informações sobre como habilitar scripts do Windows PowerShell, consulte [Executando scripts do Windows PowerShell](http://www.microsoft.com/technet/scriptcenter/topics/winpsh/manual/run.mspx).  
  
##  <a name="LoadSqlps"></a> Carregar o módulo sqlps  
 **Para carregar o módulo sqlps no Windows PowerShell**  
  
1.  Use o cmdlet **Set-ExecutionPolicy** para definir a política de execução de script adequada.  
  
2.  Use o cmdlet **Import-Module** para importar o módulo sqlps. Especifique o parâmetro **DisableNameChecking** se desejar suprimir o aviso sobre **Encode-Sqlname** e **Decode-Sqlname**.  
  
### <a name="example"></a>Exemplo  
 Este exemplo carrega o módulo **sqlps** com verificação de nome desligado.  
  
```powershell 
# Import the SQL Server Module.    
Import-Module Sqlps -DisableNameChecking;

# To check whether the module is installed.
Get-Module -ListAvailable -Name Sqlps;
```  
  
> [!NOTE]  
>  Se o módulo **sqlps** não estiver em seu caminho, altere para o local do módulo ou use o caminho completo do script (usando aspas duplas para pastas no caminho que tenham espaços). O módulo **sqlps** está localizado na pasta Tools\Powershell para a instância do SQL Server.  
  
 ![Ícone de seta usado com o link Voltar ao início](../../analysis-services/instances/media/uparrow16x16.gif "Ícone de seta usado com o link Voltar ao início") [&#91;Top&#93;]()  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)   
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [Usar cmdlets do Mecanismo de Banco de Dados](../../relational-databases/scripting/use-the-database-engine-cmdlets.md)  
 [Instalando um módulo do PowerShell](https://msdn.microsoft.com/library/dd878350(v=vs.85).aspx)  
 [Import-Module](https://technet.microsoft.com/library/hh849725.aspx)
  
  
