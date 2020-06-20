---
title: Parâmetros de Integration Services | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
helpviewer_keywords:
- Integration Services, parameters
ms.assetid: b1bb3ea3-8097-4e76-b9c2-78a0f46a23bc
author: mashamsft
ms.author: mathoma
ms.openlocfilehash: 76a5ebe7018fdc58f02a4d2454d40f172c752c4e
ms.sourcegitcommit: 57f1d15c67113bbadd40861b886d6929aacd3467
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/18/2020
ms.locfileid: "85059264"
---
# <a name="integration-services-parameters"></a>Parâmetros do Integration Services
  Para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , você pode optar por analisar [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] os pacotes no computador ou os [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] arquivos de pacote no sistema de arquivos. Se você analisar arquivos no sistema de arquivos, forneça um caminho para a pasta que contém os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
## <a name="options"></a>Opções  
 **Analisar pacotes SSIS no computador**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no computador. Por padrão, essa opção é selecionada.  
  
 **Analisar arquivos de pacote SSIS**  
 Selecione esta opção para analisar pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] no sistema de arquivos.  
  
 **Caminho para pacotes SSIS**  
 Localize um UNC ou caminho local para seus pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]. Você não tem que incluir nomes de arquivos. Se o caminho inserido não puder ser acessado, você não poderá clicar em **Avançar**. Por padrão, o caminho fica em branco. Esse campo é habilitado somente quando você seleciona **analisar arquivos de pacote SSIS**.  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o supervisor de atualização](../../../2014/sql-server/install/working-with-upgrade-advisor.md)   
 [Referência da interface de usuário do Supervisor de Atualização](../../../2014/sql-server/install/upgrade-advisor-user-interface-reference.md)  
  
  
