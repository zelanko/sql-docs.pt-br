---
title: Gerenciar modelos (SQL Server suplementos de mineração de dados) | Microsoft Docs
ms.custom: ''
ms.date: 12/29/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: analysis-services
ms.topic: conceptual
helpviewer_keywords:
- mining models, importing
- mining models, deleting
- mining models, managing
- mining models, training
- mining models, processing
- mining models, exporting
ms.assetid: c11380f0-7c24-4668-9cdf-9c53e4aff665
author: minewiskan
ms.author: owend
ms.openlocfilehash: f37939fea1188c18079fc7e619cee6a336876e24
ms.sourcegitcommit: f0772f614482e0b3cde3609e178689ce62ca3a19
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/09/2020
ms.locfileid: "84541848"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>Gerenciar Modelos (Suplementos de Mineração de Dados do SQL Server)
  ![Botão Gerenciar Modelos, faixa de opções Mineração de Dados](media/dmc-manage.gif "Botão Gerenciar Modelos, faixa de opções Mineração de Dados")  
  
 A caixa de diálogo **gerenciar modelos** permite interagir com modelos de mineração e estruturas de mineração existentes que são armazenados no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] servidor ao qual você está conectado no momento. Também é possível exibir e gerenciar estruturas e modelos temporários criados durante a sessão atual. Caso você tenha usado modelos de sessão e modelos armazenados em um servidor, os dois tipos estarão visíveis na caixa de diálogo.  
  
## <a name="using-the-manage-models-wizard"></a>Usando o Assistente para Gerenciar Modelos  
 Quando você clica em **gerenciar modelos**, a caixa de diálogo **gerenciar estruturas e modelos de mineração** é aberta, fornecendo acesso à seguinte funcionalidade para gerenciar modelos e estruturas existentes do Data Mining:  
  
-   Renomear um modelo ou uma estrutura de mineração  
  
-   Excluir um modelo ou uma estrutura de mineração  
  
-   Limpar um modelo ou uma estrutura de mineração  
  
-   Processar uma estrutura de mineração, usando dados novos ou existentes  
  
-   Exportar ou importar um modelo ou uma estrutura de mineração  
  
> [!NOTE]  
>  Não é possível criar consultas ou modelos usando essa caixa de diálogo. Para criar uma nova estrutura de mineração, use um dos assistentes fornecidos no cliente de mineração de dados para Excel ou use a **Editor avançado de consulta de mineração de dados**.  
  
### <a name="requirements"></a>Requisitos  
 Para gerenciar modelos de mineração de dados, primeiro você deve ter uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Uma conexão será necessária mesmo que você esteja trabalhando com modelos de sessão armazenados em um arquivo temporário. Para obter mais informações sobre como criar ou alterar uma conexão, consulte [conectar-se a dados de origem &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Se a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] à qual você está conectado não contiver estruturas ou modelos de mineração de dados existentes, crie esses itens usando os assistentes e outras ferramentas fornecidas por este suplemento. Você também pode criar novos modelos usando o **modelo de mineração de dados editor avançado**.  
  
## <a name="see-also"></a>Consulte Também  
 [Documentando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;suplementos de mineração de dados para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
