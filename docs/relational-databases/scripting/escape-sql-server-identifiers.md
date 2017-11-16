---
title: Retirar identificadores do SQL Server | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology: database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
caps.latest.revision: "8"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: a6bf78751fd46f1fdb4c8a4e99ff2f93f9abfdfd
ms.sourcegitcommit: 9678eba3c2d3100cef408c69bcfe76df49803d63
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/09/2017
---
# <a name="escape-sql-server-identifiers"></a>Retirar identificadores do SQL Server
  O caractere de acento grave (`) do PowerShell pode ser usado frequentemente para substituir caracteres que são permitidos nos identificadores delimitados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , mas não nomes de caminho do Windows PowerShell. Entretanto, alguns caracteres não podem ser substituídos. Por exemplo, no Windows PowerShell, não é possível substituir o caractere dois-pontos (:). Os identificadores que contém esse caractere devem ser codificados. A codificação é mais segura do que a substituição, pois os trabalhos de codificação aceitam todos os caracteres.  
  
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
  
## <a name="see-also"></a>Consulte também  
 [Identificadores do SQL Server no PowerShell](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
