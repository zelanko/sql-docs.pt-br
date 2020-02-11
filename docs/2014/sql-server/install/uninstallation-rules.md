---
title: Regras de desinstalação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
ms.assetid: 07554612-8cb6-4bd9-adde-956177261ccd
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 299a2d82464d83bf57958d6171aca1a4ba93389f
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66091737"
---
# <a name="uninstallation-rules"></a>Regras de desinstalação
  A página Regras de Desinstalação executa um conjunto de regras para garantir que a operação de Instalação pode ser concluída com êxito.  
  
 A Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] valida a configuração do computador antes da conclusão da operação de Instalação. Durante a Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o SCC (Verificador de Configuração do Sistema) examina o computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será instalado. O SCC verifica se existem condições que impedem uma operação de instalação com êxito do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Antes que a Instalação inicie o assistente de desinstalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , o SCC recupera o status de cada item. Em seguida, compara o resultado com condições necessárias e fornece orientação para a remoção de problemas de bloqueio.  
  
 A verificação da configuração do sistema gera um relatório que contém uma breve descrição de cada regra executada, bem como o status de execução. O relatório de verificação da configuração do sistema está localizado em\\[!INCLUDE[msCoName](../../includes/msconame-md.md)][!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]% ProgramFiles%\\ \120\Setup \\Bootstrap\Log<YYYYMMDD_HHMM>.  
  
 Antes de executar a operação de instalação, reveja os seguintes tópicos:  
  
1.  [Hardware and Software Requirements for Installing SQL Server 2014](hardware-and-software-requirements-for-installing-sql-server.md)  
  
2.  [Recursos compatíveis com as edições do SQL Server 2014](../../../2014/getting-started/features-supported-by-the-editions-of-sql-server-2014.md)  
  
3.  [Considerações sobre segurança para uma instalação do SQL Server](../../../2014/sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
4.  [Versões de idiomas locais no SQL Server](../../../2014/sql-server/install/local-language-versions-in-sql-server.md)  
  
 Outras referências:  
  
1.  [Atualizações de versão e edição com suporte](../../database-engine/install-windows/supported-version-and-edition-upgrades.md)  
  
2.  [Antes de instalar o cluster de failover](../failover-clusters/install/before-installing-failover-clustering.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Normas de instalação](../../../2014/sql-server/install/install-rules.md)  
  
  
