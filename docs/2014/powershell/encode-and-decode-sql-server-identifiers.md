---
title: Codificar e decodificar identificadores do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: scripting
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 373b2b9d90512293e1776d06ab5797faaf47a210
ms.sourcegitcommit: f912c101d2939084c4ea2e9881eb98e1afa29dad
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/23/2019
ms.locfileid: "72797774"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificar e decodificar identificadores do SQL Server
  Os identificadores delimitados do SQL Server às vezes contêm caracteres sem suporte em caminhos do Windows PowerShell. Esses caracteres podem ser especificados codificando seus valores hexadecimais.  
  
1.  **Before you begin:**  [Limitations and Restrictions](#LimitationsRestrictions)  
  
2.  **To process special characters:**  [Encoding an Identifier](#EncodeIdent), [Decoding an Identifier](#DecodeIdent)  
  
## <a name="before-you-begin"></a>Antes de começar  
 Os caracteres não suportados em nomes de caminho do Windows PowerShell podem ser representados, ou codificados, como o caractere "%" seguido pelo valor hexadecimal do padrão de bits que representa o caractere, como em " **%** xx". A codificação sempre pode ser usada para manipular caracteres não suportados em caminhos do Windows PowerShell.  
  
 O cmdlet **Encode-SqlName** usa um identificador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada. Ele produz uma cadeia de caracteres com todos os caracteres não suportados pela linguagem Windows PowerShell codificada com "%xx". O cmdlet **Decode-SqlName** usa um identificador codificado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada e retorna o identificador original.  
  
###  <a name="LimitationsRestrictions"></a> Limitações e restrições  
 Os cmdlets `Encode-Sqlname` e `Decode-Sqlname` só codificam ou decodificam os caracteres que são permitidos nos identificadores delimitados SQL Server, mas não tem suporte em caminhos do PowerShell. Estes são os caracteres codificados pelo **Encode-SqlName** e decodificados pelo **Decode-SqlName**:  
  
|||||||||||||  
|-|-|-|-|-|-|-|-|-|-|-|-|  
|**Caractere**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codificação hexadecimal**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|  
  
##  <a name="EncodeIdent"></a> Codificando um Identificador  
 **Para codificar um identificadores do SQL Server em um caminho PowerShell**  
  
-   Use um destes dois métodos para codificar um identificador do SQL Server:  
  
    -   Especifique o código hexadecimal para o caractere sem suporte que usa a sintaxe %XX, onde XX é o código hexadecimal.  
  
    -   Passe o identificador como uma cadeia de caracteres entre aspas para o cmdlet `Encode-Sqlname`  
  
### <a name="examples-encoding"></a>Exemplos (codificação)  
 Este exemplo especifica a versão codificada do caractere ":" (%3A):  
  
```  
Set-Location Table%3ATest  
```  
  
 Como alternativa, use **Encode-SqlName** para criar um nome com suporte no Windows PowerShell:  
  
```powershell
Set-Location (Encode-SqlName "Table:Test")  
```  
  
##  <a name="DecodeIdent"></a> Decodificando um Identificador  
 **Para decodificar um identificador do SQL Server de um caminho do PowerShell**  
  
 Use o cmdlet `Decode-Sqlname` para substituir as codificações hexadecimais pelos caracteres representados pela codificação.  
  
### <a name="examples-decoding"></a>Exemplos (decodificação)  
 Este exemplo retorna "Table:Test":  
  
```powershell
Decode-SqlName "Table%3ATest"  
```  
  
## <a name="see-also"></a>Consulte também  
 [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)   
 [Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
