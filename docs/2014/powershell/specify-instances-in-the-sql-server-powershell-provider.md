---
title: Especificar instâncias no provedor do SQL Server PowerShell | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: 9373de68-fd43-45f2-b9a6-149c96610aeb
caps.latest.revision: 7
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 4ded96666e744c72f7cae9f0f8e8f093e8e92df2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36021178"
---
# <a name="specify-instances-in-the-sql-server-powershell-provider"></a>Especificar instâncias no provedor do SQL Server PowerShell
  Os caminhos especificados para o provedor do SQL Server PowerShell devem identificar a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)] e o computador no qual ela está sendo executada. A sintaxe para especificar o computador e a instância deve obedecer as regras para identificadores do SQL Server e caminhos do Windows PowerShell.  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **Para especificar uma instância:**  [Examples](#Examples)  
  
## <a name="before-you-begin"></a>Antes de começar  
 O primeiro nó depois de SQLSERVER:\SQL em um caminho de provedor SQL Server é o nome do computador que está executando a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)]; por exemplo:  
  
```  
SQLSERVER:\SQL\MyComputer  
```  
  
 Se você está executando o Windows PowerShell no mesmo computador que a instância do [!INCLUDE[ssDE](../includes/ssde-md.md)], pode usar localhost ou (local) em vez do nome do computador. Scripts que usam localhost ou (local) podem ser executados em qualquer computador sem necessidade de alterações para refletir os nomes dos computadores diferentes.  
  
 Você pode executar várias instâncias do programa executável do [!INCLUDE[ssDE](../includes/ssde-md.md)] no mesmo computador. O nó depois do nome do computador em um caminho de provedor SQL Server identifica a instância; por exemplo:  
  
```  
SQLSERVER:\SQL\MyComputer\MyInstance  
```  
  
 Cada computador pode ter uma instância padrão do [!INCLUDE[ssDE](../includes/ssde-md.md)]. Você não especifica um nome para a instância padrão ao instalá-la. Ao especificar apenas um nome de computador em uma cadeia de conexão, você estabelecerá conexão com a instância padrão nesse computador. Todas as outras instâncias no computador devem ser instâncias nomeadas. Você especifica o nome da instância durante a configuração e as cadeias de conexão devem especificar o nome do computador e o nome da instância.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Você não pode usar um ponto (.) para especificar o computador local em scripts PowerShell. O ponto não é suportado, porque é interpretado como um comando pelo PowerShell.  
  
 Os caracteres de parêntese em (local) é tratado normalmente como comandos pelo Windows PowerShell. Você deve codificá-los ou reservá-los para uso em um caminho, ou colocar o caminho entre aspas duplas. Para obter mais informações, consulte Codifique e Decodifique Identificadores do SQL Server.  
  
 O provedor do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] requer que o nome da instância sempre seja especificado. Para instâncias padrão, especifique o nome da instância como DEFAULT.  
  
##  <a name="Examples"></a> Exemplos; Computador e nomes de instância  
 Este exemplo usa localhost e DEFAULT para especificar a instância padrão no computador local:  
  
```  
Set-Location SQLSERVER:\SQL\localhost\DEFAULT   
```  
  
 Os caracteres de parêntese em (local) é tratado normalmente como comandos pelo Windows PowerShell. Você deve:  
  
-   Incluir as cadeias de caracteres de caminho entre aspas:  
  
    ```  
    Set-Location "SQLSERVER:\SQL\(local)\DEFAULT"  
    ```  
  
-   Retirar o parêntese usando o caractere de acento grave (`):  
  
    ```  
    Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
    ```  
  
-   Codificar o parêntese usando sua representação hexadecimal:  
  
    ```  
    Set-Location SQLSERVER:\SQL\%28local%29\DEFAULT  
    ```  
  
## <a name="see-also"></a>Consulte também  
 [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  