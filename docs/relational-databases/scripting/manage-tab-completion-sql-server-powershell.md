---
title: Gerenciar o preenchimento de guias (SQL Server PowerShell) | Microsoft Docs
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- database-engine
ms.tgt_pltfrm: 
ms.topic: article
ms.assetid: 6296848a-890f-4ad3-8d9f-92ed6a79aa00
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
translationtype: Human Translation
ms.sourcegitcommit: f3481fcc2bb74eaf93182e6cc58f5a06666e10f4
ms.openlocfilehash: 310aa99b485cedf79237f993a8ffbdcffe9d2a46
ms.lasthandoff: 04/11/2017

---
# <a name="manage-tab-completion-sql-server-powershell"></a>Gerenciar conclusão de guia (SQL Server PowerShell)
  Os snap-ins do PowerShell no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresentam três variáveis (**$SqlServerMaximumTabCompletion**, **$SqlServerMaximumChildItems**e **$SqlServerIncludeSystemObjects**) para controlar o preenchimento com Tab do Windows PowerShell. A conclusão da guia reduz a quantidade de digitação necessária, retornando tabelas de itens cujos nomes iniciam com a cadeia de caracteres que você está digitando.  
  
## <a name="before-you-begin"></a>Antes de começar  
 Com a tab-completion do Windows PowerShell, quando você digita parte do nome de um caminho ou cmdlet, pode pressionar a tecla Tab para obter uma lista de itens cujos nomes correspondem aos já digitados. Em seguida, é possível selecionar o item desejado da lista sem precisar digitar o restante do nome.  
  
 Se você estiver trabalhando em um banco de dados com muitos objetos, as listas tab-completion poderão se tornar muito grandes. Alguns tipos de objetos do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , como exibições, também têm vários objetos de sistema.  
  
 Os snap-ins do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] apresentam três variáveis de sistema que podem ser usadas para controlar a quantidade de informações apresentadas por tab-completion e **Get-ChildItem**.  
  
 **$SqlServerMaximumTabCompletion =** *n*  
 Especifica o número máximo de objetos que devem ser incluídos em uma lista tab-completion. Se você selecionar Tab em um nó de caminho com mais de *n* objetos, a lista tab-completion será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  
  
 **$SqlServerMaximumChildItems =** *n*  
 Especifica o número máximo de objetos exibidos por **Get-ChildItem**. Se **Get-ChildItem** for executado em um nó de caminho com mais de *n* objetos, a lista será truncada em *n*. *n* é um inteiro. 0 é a configuração padrão e significa que não há limite para o número de objetos na lista.  
  
 **$SqlServerIncludeSystemObjects =** { **$True** | **$False** }  
 Se for **$True**, os objetos do sistema serão exibidos por tab-completion e **Get-ChildItem**. Se for **$False**, nenhum objeto de sistema será exibido. A configuração padrão é **$False**.  
  
## <a name="set-the-sql-server-tab-completion-variables"></a>Definir as variáveis de conclusão de guia do SQL Server  
 Para qualquer variável a ser alterada do valor padrão, defina a variável como o novo valor.  
  
### <a name="example-powershell"></a>Exemplo (PowerShell)  
 O exemplo a seguir define todas as três variáveis e lista suas configurações:  
  
```  
$SqlServerMaximumTabCompletion = 20  
$SqlServerMaximumChildItems = 10  
$SqlServerIncludeSystemObjects = $False  
dir variable:sqlserver*  
```  
  
## <a name="see-also"></a>Consulte também  
 [SQL Server PowerShell](../../relational-databases/scripting/sql-server-powershell.md)  
  
  
