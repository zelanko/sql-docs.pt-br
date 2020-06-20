---
title: Retirar identificadores do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: stevestein
ms.author: sstein
ms.openlocfilehash: a2b7d37e20aae20b548da83fbd32858e8192d3ae
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84960426"
---
# <a name="escape-sql-server-identifiers"></a>Retirar identificadores do SQL Server
  O caractere de acento grave (`) do PowerShell pode ser usado frequentemente para substituir caracteres que são permitidos nos identificadores delimitados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , mas não nomes de caminho do Windows PowerShell. Entretanto, alguns caracteres não podem ser substituídos. Por exemplo, no Windows PowerShell, não é possível substituir o caractere dois-pontos (:). Os identificadores que contém esse caractere devem ser codificados. A codificação é mais segura do que a substituição, pois os trabalhos de codificação aceitam todos os caracteres.  
  
## <a name="before-you-begin"></a>Antes de começar  
 O caractere de acento grave (`) geralmente encontra-se no lado esquerdo do teclado, abaixo da tecla ESC.  
  
## <a name="examples"></a>Exemplos  
 Este é um exemplo de substituição de um caractere #:  
  
```  
cd SQLSERVER:\SQL\MyComputer\MyInstance\MyDatabase\MySchema\`#MyTempTable  
```  
  
 Este é um exemplo de escape do parêntese ao especificar (local) como um nome de computador:  
  
```  
Set-Location SQLSERVER:\SQL\`(local`)\DEFAULT  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Identificadores de SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provedor de SQL Server PowerShell](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
