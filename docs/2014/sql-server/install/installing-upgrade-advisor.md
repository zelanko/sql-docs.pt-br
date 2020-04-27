---
title: Instalando o supervisor de atualização | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- installing Upgrade Advisor
- Setup [Upgrade Advisor]
- Upgrade Advisor [SQL Server], installing
ms.assetid: 1b7d6eca-1df1-47df-bbba-0fc485706a95
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 7f70d1cbb879f8fc91e48478fb820b71b51bfd2d
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66094321"
---
# <a name="installing-upgrade-advisor"></a>Instalando o Supervisor de Atualização
  O local da instalação do Supervisor de Atualização do SQL Server 2014 depende do que você analisará. O Supervisor de Atualização oferece suporte para análise remota de todos os componentes do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , com exceção do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)]. Se não estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você pode instalar o Supervisor de Atualização em qualquer computador que pode se conectar a [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], e que esteja em conformidade com [Upgrade Advisor Prerequisites](../../../2014/sql-server/install/upgrade-advisor-prerequisites.md). Se você estiver verificando instâncias do [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], será necessário instalar o Supervisor de Atualização no servidor de relatório.  
  
 Execute o arquivo **SQLUA.msi** para instalar o Supervisor de Atualização. Você pode instalar do prompt de comando para instalações autônomas e automatizadas. Consulte [Installing Upgrade Advisor from the Command Prompt](../../../2014/sql-server/install/installing-upgrade-advisor-from-the-command-prompt.md) para obter a sintaxe e exemplos.  
  
 Obter SQLUA.msi:  
  
-   Na pasta **redist** da mídia do produto [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
-   Como parte do [download do SQL 2014 Feature Pack](https://www.microsoft.com/download/details.aspx?id=42295).  
  
## <a name="uninstalling-upgrade-advisor"></a>Desinstalando o Supervisor de Atualização  
 Você pode desinstalar o Supervisor de Atualização usando **Adicionar ou Remover Programas**. A sintaxe do prompt de comando também dá suporte à remoção/desinstalação.  
  
  
