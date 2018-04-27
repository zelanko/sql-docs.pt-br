---
title: Codificar e decodificar identificadores do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: powershell
ms.service: ''
ms.component: powershell
ms.reviewer: ''
ms.suite: sql
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
ms.assetid: bb9fe0d3-e432-42d3-b324-64dc908b544a
caps.latest.revision: 7
author: stevestein
ms.author: sstein
manager: craigg
ms.workload: Inactive
ms.openlocfilehash: ce95dea671a2708f30a87ef3dcd10be0492ffe53
ms.sourcegitcommit: a85a46312acf8b5a59a8a900310cf088369c4150
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2018
---
# <a name="encode-and-decode-sql-server-identifiers"></a>Codificar e decodificar identificadores do SQL Server
[!INCLUDE[appliesto-ss-asdb-asdw-pdw-md](../includes/appliesto-ss-asdb-asdw-pdw-md.md)]

Os identificadores delimitados do SQL Server às vezes contêm caracteres que não são compatíveis com caminhos do Windows PowerShell. Esses caracteres podem ser especificados codificando seus valores hexadecimais.  

> [!NOTE]
> Há dois módulos do SQL Server PowerShell; **SqlServer** e **SQLPS**. O módulo **SQLPS** está incluído na instalação do SQL Server (para compatibilidade com versões anteriores), mas não está sendo atualizado. O módulo do PowerShell mais atualizado é o módulo do **SqlServer**. O módulo do **SqlServer** contém versões atualizadas dos cmdlets no **SQLPS** e também inclui novos cmdlets para dar suporte aos recursos mais recentes do SQL.  
> As versões anteriores do módulo do **SqlServer** *foram* incluídas no SQL Server Management Studio (SSMS), mas apenas nas versões 16.x do SSMS. Para usar o PowerShell com o SSMS 17.0 e versões posteriores, o módulo do **SqlServer** deve ser instalado da Galeria do PowerShell.
> Para instalar o módulo do **SqlServer**, consulte [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md).
  
  
Os caracteres não suportados em nomes de caminho do Windows PowerShell podem ser representados, ou codificados, como o caractere "%" seguido pelo valor hexadecimal do padrão de bits que representa o caractere, como em "**%** xx". A codificação sempre pode ser usada para manipular caracteres não suportados em caminhos do Windows PowerShell.  
  
 O cmdlet **Encode-SqlName** usa um identificador do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada. Ele produz uma cadeia de caracteres com todos os caracteres não suportados pela linguagem Windows PowerShell codificada com "%xx". O cmdlet **Decode-SqlName** usa um identificador codificado do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] como entrada e retorna o identificador original.  
  
##  <a name="LimitationsRestrictions"></a> Limitações e Restrições  
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
 [Identificadores do SQL Server no PowerShell](sql-server-identifiers-in-powershell.md)   
 [SQL Server PowerShell Provider](sql-server-powershell-provider.md)   
 [SQL Server PowerShell](sql-server-powershell.md)  
  
  
