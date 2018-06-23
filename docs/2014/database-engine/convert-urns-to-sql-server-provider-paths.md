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
ms.topic: article
ms.assetid: c9b1b8f1-b117-4e87-9704-2170f62c5c8b
caps.latest.revision: 8
author: mgblythe
ms.author: mblythe
manager: jhubbard
ms.openlocfilehash: 925eec025bb2943845748acd30e8f24693245ae2
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36118957"
---
# <a name="convert-urns-to-sql-server-provider-paths"></a>Converter URNs em caminhos de provedor SQL Server
  O modelo SMO, Objeto de Gerenciamento do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , cria nomes de recurso uniformes (URN) para seus objetos. Cada URN identifica exclusivamente um objeto SMO e pode ser convertido em um caminho de provedor do SQL Server PowerShell usando o `Convert-UrnToPath` cmdlet.  
  
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
  
  