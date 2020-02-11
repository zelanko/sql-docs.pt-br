---
title: Converter URNs em caminhos do provedor do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 77b6031e91f59fc691f0b1c055e90464d660d3a9
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "72797942"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Converter URNs em caminhos de provedor SQL Server
  O modelo SMO, Objeto de Gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , cria nomes de recurso uniformes (URN) para seus objetos. Cada URN identifica um objeto SMO exclusivamente e pode ser convertido em um caminho de provedor do SQL Server PowerShell usando o cmdlet `Convert-UrnToPath`.  
  
## <a name="converting-urns-to-paths"></a>Convertendo URNs em caminhos  
 Cada URN tem as mesmas informações, como um caminho para o objeto, mas em um formulário diferente. Por exemplo, este é o caminho para uma tabela:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 E esta é a URN para o mesmo objeto:  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Se você criou um objeto SMO em um script do PowerShell, poderá referenciar a propriedade `Urn` para obter o URN do objeto e, depois, usar o cmdlet `Convert-UrnToPath` para converter a cadeia de caracteres do URN de SMO para um caminho do Windows PowerShell. Você pode usar o provedor para navegar até locais diferentes no caminho.  
  
 Se os nomes de nó contiverem caracteres estendidos sem suporte em nomes de caminho do Windows PowerShell, o `Convert-UrnToPath` irá codificá-los em sua representação hexadecimal. Por exemplo "My:Table" será retornado como "My%3ATable".  
  
 Para obter exemplos de utilização do cmdlet, no Windows PowerShell, execute:  
  
```powershell
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Expressões de consulta e nomes de recursos uniformes](../powershell/query-expressions-and-uniform-resource-names.md)   
 [Provedor de SQL Server PowerShell](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
