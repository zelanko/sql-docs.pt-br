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
manager: craigg
ms.openlocfilehash: 100e796bb27d1e60db000a364a0432273dd5cafb
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66094241"
---
# <a name="integration-services-parameters"></a>Parâmetros do Integration Services
  Para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]o, você pode optar por [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] analisar os pacotes no computador ou [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] os arquivos de pacote no sistema de arquivos. Se você analisar arquivos no sistema de arquivos, forneça um caminho para a pasta que contém os pacotes do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)].  
  
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
  
  
