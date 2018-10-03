---
title: Modificar o serviço Avançado propriedades do SQL Server usando o VBScript | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
- docset-sql-devref
ms.topic: reference
dev_langs:
- VB
helpviewer_keywords:
- VBScript [WMI]
- modifying SQL Server Service properties
- WMI Provider for Configuration Management, VBScript
ms.assetid: f3c5d981-eaa3-4d34-9b91-37e42636aa81
author: CarlRabeler
ms.author: carlrab
manager: craigg
ms.openlocfilehash: f011dd9a1210f6f7696a95f4f34346c472a4394b
ms.sourcegitcommit: 3da2edf82763852cff6772a1a282ace3034b4936
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/02/2018
ms.locfileid: "48184316"
---
# <a name="modify-sql-server-service-advanced-properties-using-vbscript"></a>Modificar as propriedades avançadas do serviço do SQL Server usando o VBScript
  Esta seção descreve como criar um programa de VBScript que liste a versão das instâncias instaladas do [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que estiver executando em um computador.  
  
 O exemplo de código lista as instâncias de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em execução no computador e sua versão.  
  
### <a name="listing-name-and-version-of-installed-instances-of-sql-server"></a>Listando nome e versão de instâncias instaladas do SQL Server  
  
1.  Abra um documento novo em um editor de textos, como o Bloco de Notas da [!INCLUDE[msCoName](../../includes/msconame-md.md)]. Copie o código que segue esse procedimento e salve o arquivo com uma extensão .vbs. Esse exemplo é chamado test.vbs.  
  
2.  Conecte-se a uma instância do Provedor WMI para Gerenciamento do Computador com a função de VBScript `GetObject`. Este exemplo se conecta a um computador remoto denominado mpc, mas omite o nome do computador para conectar-se ao computador local: winmgmts:root\Microsoft\SqlServer\ComputerManagement. Para obter mais informações sobre a função `GetObject`, consulte a referência a VBScript.  
  
3.  Use o método `InstancesOf` para enumerar uma lista dos serviços. Os serviços também podem ser enumerados usando uma consulta de WQL simples e um método `ExecQuery`, em vez do método `InstancesOf`.  
  
4.  Use o método `ExecQuery` e uma consulta WQL para recuperar o nome e a versão das instâncias instaladas de [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
5.  Salve o arquivo.  
  
6.  Execute o script digitando `cscript test.vbs` no prompt de comando.  
  
## <a name="example"></a>Exemplo  
  
```  
set wmi = GetObject("WINMGMTS:\\.\root\Microsoft\SqlServer\ComputerManagement12")  
for each prop in wmi.ExecQuery("select * from SqlServiceAdvancedProperty where SQLServiceType = 1 AND PropertyName = 'VERSION'")  
WScript.Echo prop.ServiceName & " " & prop.PropertyName & ": " & prop.PropertyStrValue  
next  
```  
  
  
