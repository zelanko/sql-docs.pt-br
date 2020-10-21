---
title: Retirar identificadores do SQL Server
description: Em caminhos do Windows PowerShell, não há suporte para alguns caracteres que podem aparecer em identificadores delimitados pelo SQL Server. Saiba como fazer escape de alguns deles com o caractere de acento grave.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: 4ad4bdc7720d0c405e3982b6b4533b55c2756490
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005498"
---
# <a name="escape-sql-server-identifiers"></a>Retirar identificadores do SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

O caractere de escape (`) pode ser usado frequentemente para substituir caracteres que são permitidos nos identificadores delimitados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas que não são permitidos nos nomes de caminho do Windows PowerShell. Entretanto, alguns caracteres não podem ser substituídos. Por exemplo, no Windows PowerShell, não é possível substituir o caractere dois-pontos (:). Os identificadores que contém esse caractere devem ser codificados. A codificação é mais segura do que a substituição, pois os trabalhos de codificação aceitam todos os caracteres.  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

O caractere de acento grave (`) geralmente encontra-se no lado esquerdo do teclado, abaixo da tecla ESC.  

## <a name="examples"></a>Exemplos

Este é um exemplo de substituição de um caractere #:  

```powershell
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```

Este é um exemplo de escape do parêntese ao especificar (local) como um nome de computador:  

```powershell
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```

## <a name="see-also"></a>Consulte Também

- [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)
- [Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)