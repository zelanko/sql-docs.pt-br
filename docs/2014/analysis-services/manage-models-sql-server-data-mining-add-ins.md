---
title: Gerenciar modelos (SQL Server Data Mining Add-ins) | Microsoft Docs
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
manager: craigg
ms.openlocfilehash: 6d5f0619e7291cc08b1750c0b35f9639cb7a9872
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "66078034"
---
# <a name="manage-models-sql-server-data-mining-add-ins"></a>Gerenciar Modelos (Suplementos de Mineração de Dados do SQL Server)
  ![Botão de gerenciamento de modelos, faixa de opções mineração de dados](media/dmc-manage.gif "botão Gerenciar modelos, faixa de opções mineração de dados")  
  
 O **gerenciar modelos** caixa de diálogo permite que você interaja com modelos de mineração existentes e estruturas de mineração que são armazenadas no [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] server à qual você está conectado no momento. Também é possível exibir e gerenciar estruturas e modelos temporários criados durante a sessão atual. Caso você tenha usado modelos de sessão e modelos armazenados em um servidor, os dois tipos estarão visíveis na caixa de diálogo.  
  
## <a name="using-the-manage-models-wizard"></a>Usando o Assistente para Gerenciar Modelos  
 Quando você clica em **gerenciar modelos**, o **gerenciar estruturas de mineração e modelos** caixa de diálogo é aberta, fornecendo acesso às seguintes funções para gerenciar modelos de mineração de dados e estruturas existentes:  
  
-   Renomear um modelo ou uma estrutura de mineração  
  
-   Excluir um modelo ou uma estrutura de mineração  
  
-   Limpar um modelo ou uma estrutura de mineração  
  
-   Processar uma estrutura de mineração, usando dados novos ou existentes  
  
-   Exportar ou importar um modelo ou uma estrutura de mineração  
  
> [!NOTE]  
>  Não é possível criar consultas ou modelos usando essa caixa de diálogo. Para criar uma nova estrutura de mineração, use um dos assistentes fornecidos no cliente de mineração de dados para Excel, ou use o **Advanced Editor de consultas de mineração de dados**.  
  
### <a name="requirements"></a>Requisitos  
 Para gerenciar modelos de mineração de dados, primeiro você deve ter uma conexão com uma instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)]. Uma conexão será necessária mesmo que você esteja trabalhando com modelos de sessão armazenados em um arquivo temporário. Para obter mais informações sobre como criar ou alterar uma conexão, consulte [conectar-se a fonte de dados &#40;cliente de mineração de dados para Excel&#41;](connect-to-source-data-data-mining-client-for-excel.md).  
  
 Se a instância do [!INCLUDE[ssASnoversion](../includes/ssasnoversion-md.md)] à qual você está conectado não contiver estruturas ou modelos de mineração de dados existentes, crie esses itens usando os assistentes e outras ferramentas fornecidas por este suplemento. Você também pode criar novos modelos usando o **Editor de avançada de modelo de mineração de dados**.  
  
## <a name="see-also"></a>Consulte também  
 [Documentando modelos de mineração &#40;Data Mining Add-ins para Excel&#41;](documenting-mining-models-data-mining-add-ins-for-excel.md)   
 [Implantando e dimensionando modelos de mineração &#40;Data Mining Add-ins para Excel&#41;](deploying-and-scaling-mining-models-data-mining-add-ins-for-excel.md)   

  
