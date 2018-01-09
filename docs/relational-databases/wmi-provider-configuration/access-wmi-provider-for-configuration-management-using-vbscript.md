---
title: "Modificar o serviço Avançado propriedades do SQL Server usando o VBScript | Microsoft Docs"
ms.custom: 
ms.date: 03/14/2017
ms.prod: sql-non-specified
ms.prod_service: database-engine
ms.service: 
ms.component: wmi
ms.reviewer: 
ms.suite: sql
ms.technology: 
ms.tgt_pltfrm: 
ms.topic: reference
dev_langs: VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
caps.latest.revision: "17"
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.workload: Inactive
ms.openlocfilehash: 3c6e29c6279e511fa303b53392f08e10f31b00f5
ms.sourcegitcommit: f486d12078a45c87b0fcf52270b904ca7b0c7fc8
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/08/2018
---
# <a name="access-wmi-provider-for-configuration-management-using-vbscript"></a>Acessar o provedor WMI para gerenciamento de configuração usando o VBScript
[!INCLUDE[tsql-appliesto-ss2008-xxxx-xxxx-xxx-md](../../includes/tsql-appliesto-ss2008-xxxx-xxxx-xxx-md.md)]Esta seção descreve como criar um programa VBScript que liste a versão das instâncias instaladas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que são executados em um computador.  
  
 O exemplo de código lista as instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no computador e sua versão.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Listando nome e versão de instâncias instaladas do SQL Server  
  
1.  Abra um documento novo em um editor de textos, como o Bloco de Notas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copie o código que segue esse procedimento e salve o arquivo com uma extensão .vbs. Esse exemplo é chamado test.vbs.  
  
2.  Conecte-se a uma instância do Provedor WMI para Gerenciamento do Computador com a função de VBScript `GetObject`. Este exemplo se conecta a um computador remoto denominado mpc, mas omite o nome do computador para conectar-se ao computador local: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Para obter mais informações sobre a função `GetObject`, consulte a referência a VBScript.  
  
3.  Use o método `InstancesOf` para enumerar uma lista dos serviços. Os serviços também podem ser enumerados usando uma consulta de WQL simples e um método `ExecQuery`, em vez do método `InstancesOf`.  
  
4.  Use o método `ExecQuery` e uma consulta WQL para recuperar o nome e a versão das instâncias instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Salve o arquivo.  
  
6.  Execute o script digitando **cscript test.vbs** no prompt de comando.  
  
## <a name="example"></a>Exemplo  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
