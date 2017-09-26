---
title: "Configurar destino arquivo simples (Assistente de exportação e importação do SQL Server) | Microsoft Docs"
ms.custom: 
ms.date: 03/16/2017
ms.prod: sql-server-2016
ms.reviewer: 
ms.suite: 
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.impexpwizard.configureflatfiledest.f1
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.translationtype: MT
ms.sourcegitcommit: 2edcce51c6822a89151c3c3c76fbaacb5edd54f4
ms.openlocfilehash: e604c8c55cfa0bdb977840ee742d062573abeeeb
ms.contentlocale: pt-br
ms.lasthandoff: 09/26/2017

---
# <a name="configure-flat-file-destination-sql-server-import-and-export-wizard"></a>Configurar Destino Arquivo Simples (Assistente de Importação e Exportação do SQL Server)
  Se você tiver selecionado um destino de arquivo simples, o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostra Import and Export Wizard **configurar o destino de arquivo simples** depois que você especificar que você deseja copiar uma tabela ou depois de fornecer uma consulta. Nessa página, especifique opções de formatação para o arquivo simples de destino. Outra opção é examinar o mapeamento de colunas individuais e visualizar dados de exemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de tela da página Configurar Destino do Arquivo Simples  
 A captura de tela a seguir mostra um exemplo de como o **configurar o destino de arquivo simples** página do assistente.
 
 Neste exemplo, o usuário especificou opções a seguir para criar um arquivo típico de (valores separados por vírgula) de CSV.
-   **Delimitador de linha**. Cada linha de dados na saída termina com um retorno de carro-linha combinação de alimentação.
-   **Delimitador de coluna**. Colunas de dados dentro de cada linha são separadas por vírgula.

 ![Página de arquivo simples de configurar do Assistente de importação e exportação](../../integration-services/import-export-data/media/flat-file.png "página de arquivo simples de configurar do Assistente de importação e exportação")  
  
## <a name="pick-a-source-table"></a>Selecione uma tabela de origem
 **Tabela ou exibição de origem**  
-   Se você tiver especificado em uma página anterior que você deseja copiar uma tabela, selecione a tabela de origem ou exibição na lista suspensa.
-   Se você forneceu uma consulta, `"Query"` está selecionada e é a única opção.  

## <a name="specify-row-and-column-delimiters-for-the-output"></a>Especifique os delimitadores de linha e coluna para a saída
 **Delimitador de linha**  
 Selecione na lista de delimitadores para separar linhas na saída. Não há nenhuma opção para especificar um *personalizado* delimitador de linha.  
  
|Valor|Description|  
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
 Selecione na lista de delimitadores para separar as colunas na saída. Não há nenhuma opção para especificar um *personalizado* delimitador de coluna.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Delimite as colunas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|Delimite colunas com um retorno de carro.|  
|**{LF}**|Delimite colunas com uma alimentação de linha.|  
|**Ponto e vírgula {;}**|Delimite colunas com um ponto-e-vírgula.|  
|**Dois-pontos {:}**|Delimite colunas com dois-pontos.|  
|**Vírgula {,}**|Delimite colunas com uma vírgula.|  
|**Tabulação {t}**|Delimite colunas com uma tabulação.|  
|**Barra vertical {&#124;}**|Delimite colunas com uma barra vertical.|  

## <a name="optionally-review-column-mappings-and-preview-data"></a>Opcionalmente, revise os mapeamentos de coluna e visualizar dados

**Editar mapeamentos**   
Opcionalmente, clique em **editar mapeamentos** para exibir o **mapeamentos de coluna** caixa de diálogo para a tabela selecionada. Use a caixa de diálogo **Mapeamentos de Coluna** para fazer o seguinte.
-   Examine o mapeamento de colunas individuais entre a origem e o destino.
-   Copie apenas um subconjunto de colunas selecionando **ignore** para as colunas que você não deseja copiar.

Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Visualização**  
Opcionalmente, clique em **visualização** para visualizar até 200 linhas de dados de exemplo no **visualizar dados** caixa de diálogo. Isso confirma se o assistente vai copiar os dados que você deseja copiar. Para obter mais informações, consulte [Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Depois de visualizar os dados, é recomendável alterar as opções selecionadas nas páginas anteriores do assistente. Para executar essas alterações, retorne para a página **Configurar Destino do Arquivo Simples** e clique em **Voltar** para retornar às páginas anteriores, nas quais é possível alterar as seleções.  

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar as opções de formatação para o arquivo de destino simples, a próxima página é **Salvar e executar pacote**. Nesta página, especifique se deseja executar a operação imediatamente. Dependendo da configuração, você também poderá salvar as configurações como um [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pacote personalizá-lo e usá-la novamente mais tarde. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  


