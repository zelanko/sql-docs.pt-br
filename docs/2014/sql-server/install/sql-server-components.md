---
title: Componentes do SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
helpviewer_keywords:
- SQL Server Upgrade Advisor, components
- listing components to analyze
- Upgrade Advisor [SQL Server], components
- component analysis [Upgrade Advisor]
- finding components to analyze
- locating components to analyze
- detecting components to analyze
- server names [Upgrade Advisor]
- analyzing system [Upgrade Advisor], component list
- identifying components to analyze
ms.assetid: 539b9525-ce3f-4950-9146-5527a5a297ee
caps.latest.revision: 41
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: 85a89e2114cd00b28444cf6ee62d12ff1abdec42
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36119265"
---
# <a name="sql-server-components"></a>Componentes do SQL Server
  Você pode executar o Assistente para análise de Supervisor de atualização em um computador local ou remoto que tenha [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)], ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] instalado. A primeira etapa da análise de pré-atualização é identificar o computador e os componentes que serão analisados.  
  
## <a name="options"></a>Opções  
 **Nome do computador**  
 Especifica o nome do computador que será analisado. O Supervisor de atualização popula a **nome do servidor** caixa com o nome do computador local. Também é possível usar ‘.’ e ‘localhost’ para conectar ao computador local.  
  
 Para analisar um computador diferente, faça o seguinte:  
  
-   Para verificar instâncias não clusterizadas, digite o nome do computador.  
  
-   Para verificar instâncias clusterizadas, digite o nome da instância do cluster de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
-   Para verificar componentes não clusterizados que estão instalados em um nó de cluster, digite o nome do computador do nó do cluster de failover.  
  
    > [!IMPORTANT]  
    >  Não inclua o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
 Em vez de especificar o nome do computador, você pode especificar o endereço IP.  
  
 Se for verificar o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)], você deve especificar o nome do computador local. O Supervisor de Atualização verifica somente os servidores de relatório locais.  
  
 **Detectar**  
 O **detectar** botão acessa o computador especificado e detecta os componentes para analisar:  
  
-   Se você estiver analisando uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] em um computador remoto, deverá habilitar os serviços de Registro remoto no computador remoto.  
  
-   O [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] será detectado se uma instância do [!INCLUDE[ssVersion2005](../../includes/ssversion2005-md.md)], [!INCLUDE[ssKatmai](../../includes/sskatmai-md.md)], [!INCLUDE[ssKilimanjaro](../../includes/sskilimanjaro-md.md)] ou [!INCLUDE[ssSQL11](../../includes/sssql11-md.md)] for localizada no Registro do computador.  
  
-   O [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] será detectado se uma instância do [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)] for localizada no Registro do computador.  
  
-   O [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] é detectado se o [!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] for localizado no registro do computador. Entretanto, o Supervisor de Atualização verifica somente os servidores de relatório locais.  
  
 **Componentes**  
 Selecione os componentes que serão analisados. Você pode clicar no **detectar** para selecionar todos os componentes instalados no computador. Uma marca de seleção aparecerá próximo aos componentes que forem detectados como instalados no computador. Você também pode selecionar manualmente os componentes que serão analisados. Basta selecionar ou desmarcar a caixa próxima a cada componente.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  