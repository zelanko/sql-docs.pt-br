---
title: Codificar e decodificar identificadores do SQL Server | Microsoft Docs
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
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
caps.latest.revision: "7"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: c07f64624f02383e43b1e18aea1fac28338e8222
ms.sourcegitcommit: b603dcac7326bba387befe68544619e026e6a15e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/21/2017
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificar e decodificar identificadores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../../includes/appliesto-ss-asdb-asdw-pdw-md.md)] Os identificadores delimitados do SQL Server às vezes contêm caracteres que não são compatíveis em caminhos do Windows PowerShell. Esses caracteres podem ser especificados codificando seus valores hexadecimais.  
  
1.  **Antes de começar:**  [Limitações e restrições](#LimitationsRestrictions)  
  
2.  **Para processar caracteres especiais:**  [Codificando um Identificador](#EncodeIdent), [Decodificando um Identificador](#DecodeIdent)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Os caracteres não suportados em nomes de caminho do Windows PowerShell podem ser representados, ou codificados, como o caractere "%" seguido pelo valor hexadecimal do padrão de bits que representa o caractere, como em "**%**xx". A codificação sempre pode ser usada para manipular caracteres não suportados em caminhos do Windows PowerShell.  
  
 O cmdlet **Encode-SqlName** usa um identificador do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como entrada. Ele produz uma cadeia de caracteres com todos os caracteres não suportados pela linguagem Windows PowerShell codificada com "%xx". O cmdlet **Decode-SqlName** usa um identificador codificado do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] como entrada e retorna o identificador original.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
 Os cmdlets **Encode-Sqlname** e **Decode-Sqlname** só codificam ou decodificam os caracteres permitidos nos identificadores delimitados do SQL Server, mas não têm suporte em caminhos do PowerShell. Estes são os caracteres codificados pelo **Encode-SqlName** e decodificados pelo **Decode-SqlName**:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Caractere**|\|/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codificação hexadecimal**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> Codificando um Identificador  
 **Para codificar um identificadores do SQL Server em um caminho PowerShell**  
  
-   Use um destes dois métodos para codificar um identificador do SQL Server:  
  
    -   Especifique o código hexadecimal para o caractere sem suporte que usa a sintaxe %XX, onde XX é o código hexadecimal.  
  
    -   Passar o identificador como uma cadeia de caracteres entre aspas para o cmdlet **Encode-Sqlname**  
  
### <a name="examples-encoding"></a>Exemplos (codificação)  
 Este exemplo especifica a versão codificada do caractere ":" (%3A):  
  
```  
Set-Location Table%3ATest  
```  
  
 Como alternativa, use **Encode-SqlName** para criar um nome com suporte no Windows PowerShell:  
  
```  
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> Decodificando um Identificador  
 **Para decodificar um identificador do SQL Server de um caminho do PowerShell**  
  
 Use o cmdlet **Decode-Sqlname** para substituir as codificações hexadecimais pelos caracteres representados pela codificação.  
  
### <a name="examples-decoding"></a>Exemplos (decodificação)  
 Este exemplo retorna “Table:Test”:  
  
```  
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Consulte Também  
 [Identificadores do SQL Server no PowerShell](../../relational-databases/scripting/sql-server-identifiers-in-powershell.md)   
 [Provedor do SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell-provider.md)   
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
