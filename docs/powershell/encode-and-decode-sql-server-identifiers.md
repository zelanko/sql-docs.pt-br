---
title: Codificar e decodificar identificadores do SQL Server
description: Em caminhos do Windows PowerShell, não há suporte para alguns caracteres que possam ser exibidos em identificadores delimitados pelo SQL Server. Saiba como incluí-los, representando-os com os respectivos valores hexadecimais.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: a3f2ab659d77e1b06cb69905971d3954e2eb76da
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92005470"
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificar e decodificar identificadores do SQL Server

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

Os identificadores delimitados do SQL Server às vezes contêm caracteres que não são compatíveis com caminhos do Windows PowerShell. Esses caracteres podem ser especificados codificando seus valores hexadecimais.

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

Os caracteres não suportados em nomes de caminho do Windows PowerShell podem ser representados, ou codificados, como o caractere "%" seguido pelo valor hexadecimal do padrão de bits que representa o caractere, como em " **%** xx". A codificação sempre pode ser usada para manipular caracteres não suportados em caminhos do Windows PowerShell.

O cmdlet **Encode-SqlName** usa um identificador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada. Ele produz uma cadeia de caracteres com todos os caracteres não suportados pela linguagem Windows PowerShell codificada com "%xx". O cmdlet **Decode-SqlName** usa um identificador codificado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada e retorna o identificador original.  

## <a name="limitations-and-restrictions"></a>Limitações e Restrições

Os cmdlets **Encode-Sqlname** e **Decode-Sqlname** só codificam ou decodificam os caracteres permitidos nos identificadores delimitados do SQL Server, mas não têm suporte em caminhos do PowerShell. Estes são os caracteres codificados pelo **Encode-SqlName** e decodificados pelo **Decode-SqlName**:

|||||||||||||
|-|-|-|-|-|-|-|-|-|-|-|-|
|**Caractere**|\ |/|:|%|\<|>|*|?|[|]|&#124;|  
|**Codificação hexadecimal**|%5C|%2F|%3A|%25|%3C|%3E|%2A|%3F|%5B|%5D|%7C|

## <a name="encoding-an-identifier"></a>Codificando um Identificador  

### <a name="to-encode-a-sql-server-identifier-in-a-powershell-path"></a>Para codificar um identificadores do SQL Server em um caminho PowerShell

- Use um destes dois métodos para codificar um identificador do SQL Server:
    - Especifique o código hexadecimal para o caractere sem suporte que usa a sintaxe %XX, onde XX é o código hexadecimal.
    - Passar o identificador como uma cadeia de caracteres entre aspas para o cmdlet **Encode-Sqlname**

### <a name="examples-encoding"></a>Exemplos (codificação)

Este exemplo especifica a versão codificada do caractere ":" (%3A):

```powershell
Set-Location Table%3ATest
```

Como alternativa, use **Encode-SqlName** para criar um nome com suporte no Windows PowerShell:

```powershell
Set-Location (Encode-SqlName "Table:Test")
```

## <a name="decoding-an-identifier"></a>Decodificando um Identificador

### <a name="to-decode-a-sql-server-identifier-from-a-powershell-path"></a>Para decodificar um identificador do SQL Server de um caminho do PowerShell

Use o cmdlet **Decode-Sqlname** para substituir as codificações hexadecimais pelos caracteres representados pela codificação.

### <a name="examples-decoding"></a>Exemplos (decodificação)

Este exemplo retorna "Table:Test":

```powershell
Decode-SqlName "Table%3ATest"
```

## <a name="see-also"></a>Consulte Também

- [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)
- [Provedor do SQL Server PowerShell](sql-server-powershell-provider.md)
- [SQL Server PowerShell](sql-server-powershell.md)  
