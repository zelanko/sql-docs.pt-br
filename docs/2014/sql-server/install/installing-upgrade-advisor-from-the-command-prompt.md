---
title: Instalando o Supervisor de atualização do Prompt de comando | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- command prompt [Upgrade Advisor]
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: a6841cc2-ca13-4b1c-9343-9e4d54312c3a
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 4b694af5b760ae3c1ead1e4984c35ef61c0fa602
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66094342"
---
# <a name="installing-upgrade-advisor-from-the-command-prompt"></a>Instalando o Supervisor de Atualização do prompt de comando
  Você pode instalar o Supervisor de Atualização usando o Assistente de Instalação ou a partir do prompt de comando. Usando o prompt de comando, você poderá executar instalações autônomas e automatizadas.  
  
## <a name="installation-syntax"></a>Sintaxe de instalação  
 A sintaxe básica por instalar o Supervisor de Atualização a partir do prompt de comando é a seguinte:  
  
 `SQLUA.msi [options]`  
  
 A tabela a seguir mostra as opções mais comuns.  
  
|Argumento|Descrição|  
|--------------|-----------------|  
|/q[n&#124;b&#124;r&#124;f]|Define nível de interface do usuário:<br /><br /> n = nenhuma interface do usuário<br /><br /> b = interface do usuário básica (apenas progresso, nenhum prompt)<br /><br /> r = interface do usuário reduzida (caixa de diálogo ao término da instalação)<br /><br /> f = interface do usuário completa|  
|/L|Especifica as opções do arquivo de log. Para todas as mensagens de log *Nome_do_Arquivo_de_Log*, use **-L\*v**_Nome_do_Arquivo_de_Log_. Para registrar somente mensagens de erro, use `-Le` *Nome_do_Arquivo_de_Log*.|  
|ADDLOCAL=ALL&#124; REMOVE=ALL&#124;REINSTALL=ALL|Especifica a instalação (ADDLOCAL), remoção (REMOVE) ou reinstalação (REINSTALL) do Supervisor de Atualização.|  
|UAINSTALLDIR=path|Instala o Supervisor de Atualização no local especificado pelo caminho.|  
  
## <a name="installation-examples"></a>Exemplos de instalação  
 O exemplo a seguir mostra como instalar o Supervisor de Atualização usando o prompt de comando:  
  
```  
SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 Você também pode usar o programa Msiexec quando executar este comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn ADDLOCAL=ALL UAINSTALLDIR="C:\Upgrade Advisor"  
```  
  
 Isso poderá ser útil se você tiver que usar opções de instalação adicionais.  
  
## <a name="removal-examples"></a>Exemplos de remoção  
 O exemplo a seguir mostra como remover o Supervisor de Atualização usando o prompt de comando:  
  
```  
SQLUA.msi /qn REMOVE=ALL  
```  
  
 Você também pode usar o programa Msiexec quando executar este comando:  
  
```  
Msiexec.exe /i C:\Downloads\SQLUA.msi /qn REMOVE=ALL  
```  
  
## <a name="see-also"></a>Consulte também  
 [Instalando o Supervisor de atualização](../../../2014/sql-server/install/installing-upgrade-advisor.md)   
 [Pré-requisitos do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md)  
  
  
