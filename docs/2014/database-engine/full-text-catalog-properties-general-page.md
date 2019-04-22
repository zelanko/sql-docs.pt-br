---
title: Propriedades do catálogo de texto completo (página geral) | Microsoft Docs
ms.custom: ''
ms.date: 03/08/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: search
ms.topic: conceptual
f1_keywords:
- sql12.swb.fulltextsearch.ftcatalogproperties.general.f1
ms.assetid: d1f66762-2d40-4f24-b635-a417d22ee79a
author: craigg-msft
ms.author: craigg
manager: craigg
ms.openlocfilehash: be73ed98700ef261ccee026469dddd22017998e0
ms.sourcegitcommit: 323d2ea9cb812c688cfb7918ab651cce3246c296
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/18/2019
ms.locfileid: "59241445"
---
# <a name="full-text-catalog-properties-general-page"></a>Propriedades do Catálogo de Texto Completo (página Geral)
  Esta seção mostra as opções e funções disponíveis na página **Geral** da caixa de diálogo **Propriedades do Catálogo de Texto Completo** .  
  
> [!NOTE]  
>  Nos bancos de dados do [!INCLUDE[ssCurrent](../includes/sscurrent-md.md)] , um catálogo de texto completo é um conceito lógico que se refere a um grupo de índices de texto completo. O catálogo de texto completo é um objeto virtual que não pertence a nenhum grupo de arquivos.  
  
## <a name="options"></a>Opções  
  
### <a name="properties"></a>Propriedades  
 **Catálogo padrão**  
 Exibe se o catálogo é o catálogo padrão do banco de dados.  
  
 **Status de população**  
 Indica o status do catálogo. Os valores possíveis são:  
  
-   **Idle**  
  
-   **Rastreamento em andamento**  
  
-   **Em Pausa**  
  
-   **Throttled**  
  
-   **Recuperando**  
  
-   **Shutdown**  
  
-   **População incremental em andamento**  
  
-   **Criando índice**  
  
-   **Disco está em pausa completo**  
  
-   **Change tracking**  
  
 **Contagem de itens**  
 Exibe o número de itens de texto completo no catálogo.  
  
 **Tamanho do catálogo**  
 Exibe o tamanho, em megabytes, do catálogo de texto completo.  
  
 **Nome**  
 Nome do catálogo de texto completo.  
  
 **Diferenciar acentos**  
 Exibe ou modifica se o catálogo diferencia ou não marcas diacríticas, como um til (**~**), um acento agudo (**'**) ou um trema (**¨**). Os valores válidos são:  
  
-   **Não**  
  
-   **Sim**  
  
-   Para obter informações sobre sinais diacríticos, consulte [diacríticos](https://www.merriam-webster.com/dictionary/diacritic) no dicionário Webster Merriam.  
  
 **Data da última população**  
 Exibe a data em que o catálogo foi populado pela última vez.  
  
 **Proprietário**  
 Proprietário do catálogo de texto completo.  
  
 **Contagem de chaves exclusivas**  
 Número de palavras exclusivas que formam o índice de texto completo para o catálogo.  
  
### <a name="catalog-action"></a>Ação do Catálogo  
  
|||  
|-|-|  
|**Nenhum**|Não executa operações de **Otimizar catálogo**, **Recriar catálogo**nem **Repopular catálogo** .|  
|**Otimizar catálogo**|Otimiza a utilização de espaço do catálogo e melhora o desempenho de consultas. Também melhora a exatidão da classificação de relevância de resultados de pesquisa.<br /><br /> Esta ação executa ALTER FULLTEXT CATALOG *catalog_name* REORGANIZE.|  
|**Recriar catálogo**|Exclui e recria o catálogo de texto completo. Esta operação deve ser executada se uma propriedade de catálogo fundamental for alterada, como distinção de acentos.<br /><br /> Para que a recriação seja bem-sucedida, o grupo de arquivos em que reside o catálogo de texto completo deve estar online ou poder ser lido-gravado. Após a recriação, o índice de texto completo será populado novamente.<br /><br /> Esta ação executa ALTER FULLTEXT CATALOG *catalog_name* REBUILD.|  
|**Repopular catálogo**|Atualiza o catálogo com alterações recentes dos dados. Esta opção requer tempo para manutenção do catálogo.|  
  
## <a name="see-also"></a>Consulte também  
 [Popular índices de texto completo](../relational-databases/indexes/indexes.md)  
  
  
