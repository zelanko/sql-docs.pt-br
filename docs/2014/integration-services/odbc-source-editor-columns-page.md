---
title: Editor de origem ODBC (página colunas) | Microsoft Docs
ms.custom: ''
ms.date: 06/14/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.odbcsource.columns.f1
ms.assetid: 565984eb-8318-4be7-bebc-262209cf5065
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 61311dfa6428c9dd1e67fe783389c2a4b20ac1d8
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965026"
---
# <a name="odbc-source-editor-columns-page"></a>Editor de Origem ODBC (página Colunas)
  Use a página **Colunas** da caixa de diálogo do **Editor de Origem ODBC** para mapear uma coluna de saída em cada coluna externa (origem).  
  
 Para obter mais informações sobre a origem ODBC, consulte [ODBC Source](data-flow/odbc-source.md).  
  
## <a name="task-list"></a>Lista de Tarefas  
 **Para abrir a página Colunas do Editor de Origem ODBC**  
  
1.  No [!INCLUDE[ssBIDevStudio](../includes/ssbidevstudio-md.md)], abra o pacote [!INCLUDE[ssISCurrent](../includes/ssiscurrent-md.md)] que tem a fonte ODBC.  
  
2.  Na guia **Fluxo de Dados** , clique duas vezes na fonte ODBC.  
  
3.  No **Editor de Origem ODBC**, clique em **Colunas**.  
  
## <a name="options"></a>Opções  
  
### <a name="available-external-columns"></a>Colunas Externas Disponíveis  
 A lista de colunas externas disponíveis na fonte de dados. Você não pode usar esta tabela para adicionar ou excluir colunas. Selecionar as colunas a serem usadas da origem. As colunas selecionadas são adicionadas à lista **Coluna Externa** na ordem em que são selecionadas.  
  
 Marque essa caixa de seleção **Selecionar Tudo** para selecionar todas as colunas.  
  
### <a name="external-column"></a>Coluna Externa  
 Uma exibição das colunas externas (origem) na ordem em que serão exibidas ao configurar os componentes que consomem os dados da origem ODBC.  
  
### <a name="output-column"></a>Coluna de Saída  
 Insira um nome exclusivo para cada coluna de saída. O padrão é o nome da coluna externa (origem) selecionada; porém, é possível escolher qualquer nome descritivo exclusivo. O nome inserido é exibido no Designer SSIS.  
  
## <a name="see-also"></a>Consulte Também  
 [Editor de origem ODBC &#40;página Gerenciador de conexões&#41;](../../2014/integration-services/odbc-source-editor-connection-manager-page.md)   
 [Editor de Fonte ODBC &#40;Página Saída de Erro&#41;](../../2014/integration-services/odbc-source-editor-error-output-page.md)  
  
  
