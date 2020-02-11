---
title: Execução de opções de consulta (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: database-engine
ms.topic: conceptual
f1_keywords:
- sql12.swb.query.general.f1
ms.assetid: 858a0263-2f04-4692-b8bf-63e93c998ead
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: b3ecf106315fa88fdfb68599cfce71a77be975dd
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "66089039"
---
# <a name="query-options-execution-general-page"></a>Execução de Opções de Consultas (página Geral)
  Use esta página para especificar as opções de execução [!INCLUDE[msCoName](../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] de consultas. Para acessar essa caixa de diálogo, clique com o botão direito do mouse no corpo de uma janela do Editor de Consultas e clique em **Opções de Consultas**.  
  
## <a name="uielement-list"></a>Lista de elementos de interface do usuário  
 **SET ROWCOUNT**  
 O valor padrão 0 indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esperará por resultados até que todos os resultados tenham sido recebidos. Forneça um valor maior que 0 se desejar que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pare a consulta após obter o número especificado de linhas. Para desligar essa opção (de forma que todas as linhas sejam retornadas), especifique SET ROWCOUNT 0.  
  
 **DEFINIR TEXTSIZE**  
 O valor padrão de 2.147.483.647 bytes indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecerá um campo de dados completo até o limite dos campos de dados `text`, `ntext`, `nvarchar(max)` e `varchar(max)`. Não afeta o tipo de dados XML. Forneça um número menor para limitar os resultados no caso de valores grandes. Colunas maiores que o número fornecido serão truncadas.  
  
 **Tempo limite de execução**  
 Indica o número de segundos para aguardar antes de cancelar a consulta. Um valor 0 indica uma espera infinita ou nenhum tempo limite.  
  
 **Separador de lotes**  
 Digite uma palavra que você usa para separar instruções Transact-SQL em lotes. O padrão é GO.  
  
 **Por padrão, abra novas consultas no modo SQLCMD**  
 Marque esta caixa de seleção para abrir novas consultas no modo SQLCMD. Essa caixa de seleção só é visível quando a caixa de diálogo é aberta pelo menu **Ferramentas** .  
  
 Ao selecionar essa opção, esteja atento às seguintes limitações:  
  
-   O IntelliSense está desativado no Editor de Consultas do [!INCLUDE[ssDE](../includes/ssde-md.md)] .  
  
-   Como o Editor de Consultas não é executado na linha de comando, você não pode passar parâmetros de linha de comando, como variáveis.  
  
-   Como o Editor de Consultas não pode responder a prompts do sistema operacional, você deve ter cuidado para não executar instruções interativas.  
  
 **Redefinir para padrão**  
 Redefine todos os valores dessa página com os valores padrão originais.  
  
  
