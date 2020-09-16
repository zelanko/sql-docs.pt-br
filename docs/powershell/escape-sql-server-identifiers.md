---
title: Retirar identificadores do SQL Server | Microsoft Docs
description: Em caminhos do Windows PowerShell, não há suporte para alguns caracteres que possam ser exibidos em identificadores delimitados pelo SQL Server. Saiba como fazer escape de alguns deles com o caractere de acento grave.
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 8a73e945-daa6-4e5d-93da-10f000f1f3a2
author: markingmyname
ms.author: maghan
ms.openlocfilehash: c7896c2f0368826698b29aab5d1f8d52ae9ad22d
ms.sourcegitcommit: a9f16d7819ed0e2b7ad8f4a7d4d2397437b2bbb2
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 08/21/2020
ms.locfileid: "88714034"
---
# <a name="escape-sql-server-identifiers"></a>Retirar identificadores do SQL Server
[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

O caractere de escape (`) pode ser usado frequentemente para substituir caracteres que são permitidos nos identificadores delimitados do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)], mas que não são permitidos nos nomes de caminho do Windows PowerShell. Entretanto, alguns caracteres não podem ser substituídos. Por exemplo, no Windows PowerShell, não é possível substituir o caractere dois-pontos (:). Os identificadores que contém esse caractere devem ser codificados. A codificação é mais segura do que a substituição, pois os trabalhos de codificação aceitam todos os caracteres.  

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).

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
 [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
