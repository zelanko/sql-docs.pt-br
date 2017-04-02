---
title: "Verificar par&#226;metros do Verificador de Configura&#231;&#227;o do Sistema | Microsoft Docs"
ms.custom: ""
ms.date: "03/14/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "setup-install"
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "instalando o SQL Server, verificações de configuração do sistema"
  - "verificadores de configuração do sistema com falhas [SQL Server]"
  - "verificando configuração antes da instalação"
  - "SCC [SQL Server]"
  - "verificador de configuração do sistema"
  - "examinando computador antes da instalação [SQL Server]"
  - "verificando configuração antes da instalação"
  - "informações de status [SQL Server], verificador de configuração do sistema"
  - "parâmetros [SQL Server], verificador de configuração do sistema"
  - "verificadores de configuração [SQL Server]"
  - "Instalação [SQL Server], verificador de configuração do sistema"
ms.assetid: 8e712c15-6bfa-4d71-b303-9526101e5594
caps.latest.revision: 46
author: "MikeRayMSFT"
ms.author: "mikeray"
manager: "jhubbard"
caps.handback.revision: 46
---
# Verificar par&#226;metros do Verificador de Configura&#231;&#227;o do Sistema
  Durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SCC (Verificador de Configuração do Sistema) examina o computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será instalado. O SCC verifica se existem condições que impedem uma instalação com êxito do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Antes que a Instalação inicie o Assistente de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], o SCC recupera o status de cada item. Em seguida, compara o resultado com condições necessárias e fornece orientação para a remoção de problemas de bloqueio.  
  
 O verificador da configuração do sistema gera um relatório que contém uma breve descrição de cada regra executada, bem como o status de execução. O relatório de verificação da configuração do sistema está localizado em %programfiles%\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]\130\Setup Bootstrap\Log\\<AAAAMMDD_HHMM>\\.  
  
## Consulte também  
 [Requisitos de hardware e software para a instalação do SQL Server 2016](../../sql-server/install/hardware-and-software-requirements-for-installing-sql-server-2016.md)   
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)   
 [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
  