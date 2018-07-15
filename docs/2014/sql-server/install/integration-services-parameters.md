---
title: Parâmetros do Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
caps.latest.revision: 6
author: mashamsft
ms.author: mathoma
manager: craigg
ms.openlocfilehash: 15d484ffbd513ac8a14f4388cd3cdce897654164
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37282552"
---
# <a name="integration-services-parameters"></a>Parâmetros do Integration Services
  Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode optar por analisar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes no computador, ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] arquivos de pacote no sistema de arquivos. Se você analisar arquivos no sistema de arquivos, forneça um caminho para a pasta que contém os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Analisar pacotes SSIS no computador**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no computador. Por padrão, essa opção é selecionada.  
  
 **Analisar arquivos de pacote do SSIS**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no sistema de arquivos.  
  
 **Caminho para pacotes do SSIS**  
 Localize um UNC ou caminho local para seus pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Você não tem que incluir nomes de arquivos. Se o caminho inserido não pode ser acessado, você não poderá clicar em **próxima**. Por padrão, o caminho fica em branco. Esse campo é habilitado somente quando você seleciona **arquivos de pacote SSIS analisar**.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
