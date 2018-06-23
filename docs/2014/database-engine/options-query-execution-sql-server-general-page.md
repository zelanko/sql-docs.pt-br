---
title: Opções (página gerais do servidor SQL de execução da consulta) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- VS.ToolsOptionsPages.QueryExecution.SqlServer.SqlExecutionGeneral
ms.assetid: 3f8d59bc-3f97-4e5d-8b86-5ac670d20780
caps.latest.revision: 33
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: 809a3a2d681285a0a0f02e6ca9ac18497ae28804
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36120409"
---
# <a name="options-query-execution-sql-server-general-page"></a>Opções (página gerais do servidor SQL de execução da consulta)
  Use essa página a fim de especificar as opções para executar consultas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . As alterações feitas nessas opções são aplicadas apenas a novas consultas do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] . Para alterar as opções de uma consulta atual, clique em **Opções de Consulta** no menu **Consulta** ou clique com o botão direito do mouse em uma janela Consulta do [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] e selecione **Opções de Consulta**.  
  
## <a name="options"></a>Opções  
 **SET ROWCOUNT**  
 O valor padrão 0 indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] esperará por resultados até que todos os resultados tenham sido recebidos. Forneça um valor maior que 0 se desejar que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] pare a consulta após obter o número especificado de linhas. Para desligar essa opção (de forma que todas as linhas sejam retornadas), especifique SET ROWCOUNT 0.  
  
 **SET TEXTSIZE**  
 O valor padrão de 2.147.483.647 bytes, indica que o [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] fornecerá campos de dados completos até o limite dos campos de dados `text` e `ntext`. Forneça um número menor para limitar os resultados no caso de valores grandes. Colunas maiores que o número fornecido serão truncadas.  
  
 **Tempo limite de execução**  
 Define o valor padrão na caixa de diálogo **Nova Conexão** . Use essa caixa de rotação para informar ao [!INCLUDE[ssNoVersion](../includes/ssnoversion-md.md)] o número de segundos de espera antes de cancelar a consulta. Um valor 0 indica uma espera infinita ou nenhum tempo limite. Esse valor é 0 em uma nova instalação.  
  
 **Separador de lotes**  
 Digite uma palavra que você usa para separar instruções [!INCLUDE[tsql](../includes/tsql-md.md)] em lotes. O padrão é GO.  
  
 **Por padrão, abrir novas consultas no modo SQLCMD**  
 Marque esta caixa de seleção para abrir novas consultas no modo SQLCMD. Para obter mais informações sobre o modo SQLCMD, consulte [Editar scripts SQLCMD com o Editor de Consultas](../relational-databases/scripting/edit-sqlcmd-scripts-with-query-editor.md).  
  
 Ao selecionar essa opção, esteja atento às seguintes limitações:  
  
-   O IntelliSense está desativado no Editor de Consultas do [!INCLUDE[ssDE](../includes/ssde-md.md)] .  
  
-   Como o Editor de Consultas não é executado na linha de comando, você não pode passar parâmetros de linha de comando, como variáveis.  
  
-   Como o Editor de Consultas não pode responder a prompts do sistema operacional, você deve ter cuidado para não executar instruções interativas.  
  
 **Redefinir para padrão**  
 Clique para restaurar todos os valores dessa página aos seus valores padrão originais.  
  
## <a name="see-also"></a>Consulte também  
 [sqlcmd Utility](../tools/sqlcmd-utility.md)  
  
  