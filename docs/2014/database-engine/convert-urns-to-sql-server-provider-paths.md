---
title: Converter URNs em caminhos do provedor do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
caps.latest.revision: 8
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: c0f82e3bb4185a29a8a40247da8ef7533b3d281c
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37224095"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Converter URNs em caminhos de provedor SQL Server
  O modelo SMO, Objeto de Gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , cria nomes de recurso uniformes (URN) para seus objetos. Cada URN identifica exclusivamente um objeto do SMO e pode ser convertido em um caminho de provedor do SQL Server PowerShell usando o `Convert-UrnToPath` cmdlet.  
  
## <a name="converting-urns-to-paths"></a>Convertendo URNs em caminhos  
 Cada URN tem as mesmas informações, como um caminho para o objeto, mas em um formulário diferente. Por exemplo, este é o caminho para uma tabela:  
  
 SQLSERVER:\SQL\MyComputer\DEFAULT\Databases\AdventureWorks2012\Tables\Person.Address  
  
 E esta é a URN para o mesmo objeto:  
  
 Server[@Name='MyComputer']\Database[@Name='AdventureWorks2012']\Table[@Name='Address' and @Schema='Person']  
  
 Se você criou um objeto SMO em um script do PowerShell, poderá referenciar a propriedade `Urn` para obter o URN do objeto e, depois, usar o cmdlet `Convert-UrnToPath` para converter a cadeia de caracteres do URN de SMO para um caminho do Windows PowerShell. Você pode usar o provedor para navegar até locais diferentes no caminho.  
  
 Se os nomes de nó contiverem caracteres estendidos sem suporte em nomes de caminho do Windows PowerShell, o `Convert-UrnToPath` irá codificá-los em sua representação hexadecimal. Por exemplo "My:Table" será retornado como "My%3ATable".  
  
 Para obter exemplos de utilização do cmdlet, no Windows PowerShell, execute:  
  
```  
Get-Help Convert-UrnToPath -Examples  
```  
  
## <a name="see-also"></a>Consulte também  
 [Expressões de consultas e nomes de recursos uniformes](../powershell/query-expressions-and-uniform-resource-names.md)   
 [Provedor do SQL Server PowerShell](../powershell/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../powershell/sql-server-powershell.md)  
  
  
