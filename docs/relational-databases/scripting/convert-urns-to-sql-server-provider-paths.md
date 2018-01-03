---
title: Converter URNs em caminhos do provedor do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: sql-tools
ms.service: 
ms.component: ssms-scripting
ms.reviewer: 
ms.suite: sql
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: dc1a1168400eb47d8d9a655486506c87ec939e86
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Converter URNs em caminhos de provedor SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] O modelo SMO (Objeto de Gerenciamento do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]) cria URNs (nomes de recurso uniformes) para seus objetos. Cada URN identifica um objeto SMO exclusivamente e pode ser convertido em um caminho de provedor do SQL Server PowerShell usando o cmdlet **Convert-UrnToPath** .  
  
## <a name="converting-urns-to-paths"></a>Convertendo URNs em caminhos  
 Cada URN tem as mesmas informações, como um caminho para o objeto, mas em um formulário diferente. Por exemplo, este é o caminho para uma tabela:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 E esta é a URN para o mesmo objeto:  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Se você tiver criado um objeto SMO em um script do PowerShell, poderá referenciar a propriedade **Convert-UrnToPath** para obter o URN do objeto e usar o cmdlet **Convert-UrnToPath** para converter a cadeia do URN do SMO em um caminho do Windows PowerShell. Você pode usar o provedor para navegar até locais diferentes no caminho.  
  
 Se os nomes de nó contiverem caracteres estendidos sem suporte em nomes de caminho do Windows PowerShell, o **Convert-UrnToPath** vai codificá-los em suas representações hexadecimais. Por exemplo "My:Table" será retornado como "My%3ATable".  
  
 Para obter exemplos de utilização do cmdlet, no Windows PowerShell, execute:  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões de consultas e nomes de recursos uniformes](../../powershell/query-expressions-and-uniform-resource-names.md)   
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
