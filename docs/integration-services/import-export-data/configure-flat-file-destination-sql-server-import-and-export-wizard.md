---
title: Configurar destino de arquivo simples (Assistente de Importação e Exportação do SQL Server) | Microsoft Docs
ms.custom: ''
ms.date: 03/16/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 10d89181165d76e0b48dd7b09f0508d3d9f77419
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35408518"
---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar Destino Arquivo Simples (Assistente de Importação e Exportação do SQL Server)
  Se você tiver selecionado um destino de arquivo simples, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Configurar Destino do Arquivo Simples** depois que você especificar que deseja copiar uma tabela ou depois de fornecer uma consulta. Nessa página, especifique opções de formatação para o arquivo simples de destino. Outra opção é examinar o mapeamento de colunas individuais e visualizar dados de exemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de tela da página Configurar Destino do Arquivo Simples  
 A captura de tela a seguir mostra um exemplo da página **Configurar Destino do Arquivo Simples** do assistente.
 
 Neste exemplo, o usuário especificou as opções a seguir para criar um arquivo CSV (valores separados por vírgula) típico.
-   **Delimitador de linha**. Cada linha de dados na saída termina com uma combinação de retorno de carro e alimentação de linha.
-   **Delimitador de coluna**. Colunas de dados dentro de cada linha são separadas com uma vírgula.

 ![Configurar a página de arquivo simples do Assistente de Importação e Exportação](../../integration-services/import-export-data/media/flat-file.png)
  
## <a name="pick-a-source-table"></a>Selecionar uma tabela de origem
 **Tabela ou exibição de origem**  
-   Se você tiver especificado em uma página anterior que você deseja copiar uma tabela, selecione a exibição ou tabela de origem na lista suspensa.
-   Se você forneceu uma consulta, `"Query"` está selecionada e é a única opção.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Especificar os delimitadores de linha e de coluna para a saída
 **Delimitador de linha**  
 Selecione da lista de delimitadores para separar linhas na saída. Não há nenhuma opção para especificar um delimitador de linha *personalizado*.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|Delimite as linhas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|Delimite linhas com um retorno de carro.|  
|**{LF}**|Delimite linhas com uma alimentação de linha.|  
|**Ponto e vírgula {;}**|Delimite linhas com um ponto-e-vírgula.|  
|**Dois-pontos {:}**|Delimite linhas com dois-pontos.|  
|**Vírgula {,}**|Delimite linhas com uma vírgula.|  
|**Tabulação {t}**|Delimite linhas com uma tabulação.|  
|**Barra vertical {&#124;}**|Delimite linhas com uma barra vertical.|  
  
 **Delimitador de coluna**  
 Selecione da lista de delimitadores para separar colunas na saída. Não há nenhuma opção para especificar um delimitador de coluna *personalizado*.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|Delimite as colunas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|Delimite colunas com um retorno de carro.|  
|**{LF}**|Delimite colunas com uma alimentação de linha.|  
|**Ponto e vírgula {;}**|Delimite colunas com um ponto-e-vírgula.|  
|**Dois-pontos {:}**|Delimite colunas com dois-pontos.|  
|**Vírgula {,}**|Delimite colunas com uma vírgula.|  
|**Tabulação {t}**|Delimite colunas com uma tabulação.|  
|**Barra vertical {&#124;}**|Delimite colunas com uma barra vertical.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, examine os mapeamentos de coluna e visualize os dados

**Editar mapeamentos**   
Opcionalmente, clique em **Editar mapeamentos** para exibir a caixa de diálogo **Mapeamentos de Coluna** para a tabela selecionada. Use a caixa de diálogo **Mapeamentos de Coluna** para fazer o seguinte.
-   Examine o mapeamento de colunas individuais entre a origem e o destino.
-   Copie apenas um subconjunto de colunas selecionando **ignore** para as colunas que você não deseja copiar.

Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Visualização**  
Opcionalmente, clique em **Visualização** para visualizar até 200 linhas de dados de exemplo na caixa de diálogo **Visualizar Dados**. Isso confirma se o assistente vai copiar os dados que você deseja copiar. Para obter mais informações, consulte [Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Depois de visualizar os dados, é recomendável alterar as opções selecionadas nas páginas anteriores do assistente. Para executar essas alterações, retorne para a página **Configurar Destino do Arquivo Simples** e clique em **Voltar** para retornar às páginas anteriores, nas quais é possível alterar as seleções.  

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar as opções de formatação para o arquivo de destino simples, a próxima página é **Salvar e executar pacote**. Nesta página, especifique se deseja executar a operação imediatamente. Dependendo da sua configuração, você também poderá salvar suas configurações como um pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  

