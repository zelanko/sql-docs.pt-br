---
title: Instalando o Supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 82db1c6f36d8b03d2a603c0a616090ec9d3544af
ms.sourcegitcommit: 334cae1925fa5ac6c140e0b2c38c844c477e3ffb
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/13/2018
ms.locfileid: "53353996"
---
# <a name="installing-upgrade-advisor"></a>Instalando o Supervisor de Atualização
  O local da instalação do Supervisor de Atualização do SQL Server 2014 depende do que você analisará. O Supervisor de Atualização oferece suporte para análise remota de todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , com exceção do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se não estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode instalar o Supervisor de Atualização em qualquer computador que pode se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e que esteja em conformidade com [Upgrade Advisor Prerequisites](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md). Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 Execute o arquivo **SQLUA.msi** para instalar o Supervisor de Atualização. Você pode instalar do prompt de comando para instalações autônomas e automatizadas. Consulte [Installing Upgrade Advisor from the Command Prompt](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) para obter a sintaxe e exemplos.  
  
 Obter SQLUA.msi:  
  
-   Na pasta **redist** da mídia do produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Como parte do [download do SQL 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295).  
  
## <a name="uninstalling-upgrade-advisor"></a>Desinstalando o Supervisor de Atualização  
 Você pode desinstalar o Supervisor de Atualização usando **Adicionar ou Remover Programas**. A sintaxe do prompt de comando também dá suporte à remoção/desinstalação.  
  
  
