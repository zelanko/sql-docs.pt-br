---
title: Gerenciar conclusão de guia (SQL Server PowerShell)
description: Saiba como controlar o preenchimento com Tab do Windows PowerShell fazendo uso adequado de três variáveis nos módulos do SQL Server PowerShell.
ms.prod: sql
ms.technology: sql-server-powershell
ms.topic: conceptual
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
author: markingmyname
ms.author: maghan
ms.reviewer: matteot, drskwier
ms.custom: ''
ms.date: 10/14/2020
ms.openlocfilehash: d15d859239aa9ea36f0885218d3469489f28a9b2
ms.sourcegitcommit: a5398f107599102af7c8cda815d8e5e9a367ce7e
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/13/2020
ms.locfileid: "92006085"
---
# <a name="manage-tab-completion-with-sql-server-powershell"></a>Gerenciar o preenchimento com Tab com o SQL Server PowerShell

[!INCLUDE[SQL Server Azure SQL Database Synapse Analytics PDW ](../includes/applies-to-version/sql-asdb-asdbmi-asa-pdw.md)]

 Os snap-ins do PowerShell no [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] apresentam três variáveis (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems** e **$SqlServerIncludeSystemObjects**) para controlar o preenchimento com Tab do Windows PowerShell. A conclusão da guia reduz a quantidade de digitação necessária, retornando tabelas de itens cujos nomes iniciam com a cadeia de caracteres que você está digitando.  

[!INCLUDE [sql-server-powershell-version](../includes/sql-server-powershell-version.md)]

Com a tab-completion do Windows PowerShell, quando você digita parte do nome de um caminho ou cmdlet, pode pressionar a tecla Tab para obter uma lista de itens cujos nomes correspondem aos já digitados. Em seguida, é possível selecionar o item desejado da lista sem precisar digitar o restante do nome.  

Se você estiver trabalhando em um banco de dados com muitos objetos, as listas tab-completion poderão se tornar grandes. Alguns tipos de objetos do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] , como exibições, também têm vários objetos de sistema.  

Os snap-ins do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] apresentam três variáveis de sistema que podem ser usadas para controlar a quantidade de informações apresentadas por tab-completion e **Get-ChildItem**.

## <a name="sqlservermaximumtabcompletion--n"></a>$SqlServerMaximumTabCompletion =** *n*

Especifica o número máximo de objetos que devem ser incluídos em uma lista tab-completion. Se você selecionar Tab em um nó de caminho com mais de *n* objetos, a lista tab-completion será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  

## <a name="sqlservermaximumchilditems--n"></a>$SqlServerMaximumChildItems =** *n*

Especifica o número máximo de objetos exibidos por **Get-ChildItem**. Se **Get-ChildItem** for executado em um nó de caminho com mais de *n* objetos, a lista será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  

## <a name="sqlserverincludesystemobjects---true--false-"></a>$SqlServerIncludeSystemObjects =** { **$True** | **$False** }

Se for **$True**, os objetos do sistema serão exibidos por tab-completion e **Get-ChildItem**. Se for **$False**, nenhum objeto de sistema será exibido. A configuração padrão é **$False**.  

## <a name="set-the-sql-server-tab-completion-variables"></a>Definir as variáveis de conclusão de guia do SQL Server

Para qualquer variável a ser alterada do valor padrão, defina a variável como o novo valor.  

### <a name="example-powershell"></a>Exemplo (PowerShell)

O exemplo a seguir define todas as três variáveis e lista suas configurações:  

```powershell
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```

## <a name="see-also"></a>Consulte Também

- [Instalar o SQL Server PowerShell](download-sql-server-ps-module.md)
- [SQL Server PowerShell](sql-server-powershell.md)