---
title: Divisor de CDC | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.ssis.designer.cdcsplitter.f1
ms.assetid: 167bc5c6-fa36-439d-987c-b20acd1a77e2
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 290cc29a8bdf4ebb3a7b8cd0e4d2c3c11610987a
ms.sourcegitcommit: 34278310b3e005d008cd2106a7b86fc6e736f661
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/26/2020
ms.locfileid: "85432353"
---
# <a name="cdc-splitter"></a>Separador de CDC
  O separador de CDC divide um único fluxo de linhas de alteração de um fluxo de dados de origem CDC em diferentes fluxos de dados para operações de Inserir, Atualizar e Excluir. O fluxo de dados é dividido com base na coluna necessária de `__$operation` e seus valores padrão em tabelas de alterações do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] .  
  
|Valor da operação|Saída|DESCRIÇÃO|  
|------------------------|------------|-----------------|  
|1|Excluir|Linha excluída|  
|2|Insert|Linha inserida (não disponível durante o uso do modo de CDC **Rede com Mesclagem** )|  
|3|Atualizar|Linha Before-update (disponível apenas durante o uso do modo de CDC **Tudo com Valores Antigos** )|  
|4|Atualizar|Linha After-update (após Before-update)|  
|5|Atualizar|Linha Merge (disponível apenas durante o uso do modo CDC **Rede com Mesclagem** )|  
|Outros|Erro||  
  
 Você pode usar o separador para se conectar a saídas INSERT, DELETE e UPDATE predefinidas para processamento adicional.  
  
 A transformação de Separador de CDC tem uma entrada e uma saída comum.  
  
## <a name="error-handling"></a>Tratamento de erros  
 A transformação do Separador de CDC tem uma saída de erro. As linhas Input com um valor inválido da coluna $operation são consideradas errôneas e são tratadas de acordo com a propriedade **ErrorRowDisposition** da entrada.  
  
 A saída de erro de componente inclui as colunas de saída seguintes:  
  
-   **Código de Erro**: definida como 1.  
  
-   **Coluna de Erro**: a coluna de origem que causa o erro (para erros de conversão).  
  
-   **Colunas de Linha de erro**: as colunas de entrada da linha que causou o erro.  
  
## <a name="configuring-the-cdc-splitter"></a>Configurando o Separador de CDC  
 Não há nenhuma propriedade configurável para o separador de CDC.  
  
 Para obter mais informações sobre como usar o separador de CDC, consulte Componentes de CDC para Microsoft SQL Server Integration Services.  
  
 A caixa de diálogo **Editor Avançado** contém as propriedades que podem ser definidas programaticamente.  
  
 Para abrir a caixa de diálogo **Editor Avançado** :  
  
-   Na tela **Fluxo de Dados** do seu projeto do [!INCLUDE[ssISCurrent](../../includes/ssiscurrent-md.md)] , clique com o botão direito do mouse no separador de CDC e selecione **Mostrar Editor Avançado**.  
  
## <a name="see-also"></a>Consulte Também  
 [Direcionar o fluxo de CDC de acordo com o tipo de alteração](direct-the-cdc-stream-according-to-the-type-of-change.md)  
  
  
