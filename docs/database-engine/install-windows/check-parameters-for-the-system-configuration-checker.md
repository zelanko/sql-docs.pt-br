---
title: Verificar parâmetros do Verificador de Configuração do Sistema | Microsoft Docs
ms.custom: ''
ms.date: 09/05/2017
ms.prod: sql
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
helpviewer_keywords:
- installing SQL Server, system configuration checks
- failed system configuration checks [SQL Server]
- verifying configuration before installation
- SCC [SQL Server]
- system configuration checker
- scanning computer before installation [SQL Server]
- checking configuration before installation
- status information [SQL Server], system configuration checker
- parameters [SQL Server], system configuration checker
- configuration checkers [SQL Server]
- Setup [SQL Server], system configuration checker
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
author: MashaMSFT
ms.author: mathoma
monikerRange: '>=sql-server-2016||=sqlallproducts-allversions'
manager: jroth
ms.openlocfilehash: 90afaab67be4e46488ee188f67447c2e30d03dfd
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66795016"
---
# <a name="check-parameters-for-the-system-configuration-checker"></a>Verificar parâmetros do Verificador de Configuração do Sistema

[!INCLUDE[appliesto-ss-xxxx-xxxx-xxx-md-winonly](../../includes/appliesto-ss-xxxx-xxxx-xxx-md-winonly.md)]

Durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o SCC (Verificador de Configuração do Sistema) examina o computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será instalado. O SCC verifica se existem condições que impedem uma instalação com êxito do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes que a Instalação inicie o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o SCC recupera o status de cada item. Em seguida, compara o resultado com condições necessárias e fornece orientação para a remoção de problemas de bloqueio.  
  
O verificador da configuração do sistema gera um relatório que contém uma breve descrição de cada regra executada, bem como o status de execução. O relatório de verificação da configuração do sistema está localizado em %programfiles%\Microsoft SQL Server\140\Setup Bootstrap\Log\\\<YYYYMMDD_HHMM>\\\.    
  
Para obter mais informações, consulte os links a seguir:

- [Requisitos de Hardware e Software para a Instalação do SQL Server](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server.md)   
- [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
- [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  
