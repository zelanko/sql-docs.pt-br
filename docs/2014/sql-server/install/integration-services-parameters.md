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
ms.topic: article
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
caps.latest.revision: 6
author: JennieHubbard
ms.author: jhubbard
manager: jhubbard
ms.openlocfilehash: f178c02cc93d23a14e0fb658398e5f0ba4cf6dc0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36011279"
---
# <a name="integration-services-parameters"></a>Parâmetros do Integration Services
  Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)], você pode optar por analisar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacotes no computador, ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] arquivos de pacote no sistema de arquivos. Se você analisar arquivos no sistema de arquivos, forneça um caminho para a pasta que contém os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Analisar pacotes SSIS no computador**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no computador. Por padrão, essa opção é selecionada.  
  
 **Analisar arquivos de pacote SSIS**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no sistema de arquivos.  
  
 **Caminho para pacotes do SSIS**  
 Localize um UNC ou caminho local para seus pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Você não tem que incluir nomes de arquivos. Se o caminho inserido não pode ser acessado, você não pode clicar em **próximo**. Por padrão, o caminho está em branco. Este campo só é habilitado quando você seleciona **arquivos de pacote SSIS analisar**.  
  
## <a name="see-also"></a>Consulte também  
 [Trabalhando com o Supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência de Interface de usuário do Supervisor de atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  