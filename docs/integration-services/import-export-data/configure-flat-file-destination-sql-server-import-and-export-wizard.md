---
title: "Configurar Destino Arquivo Simples (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server) | Microsoft Docs"
ms.custom: ""
ms.date: "03/16/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.impexpwizard.configureflatfiledest.f1"
ms.assetid: 318e8da0-37d3-46cd-943a-fc5d66aad93a
caps.latest.revision: 53
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 50
---
# Configurar Destino Arquivo Simples (Assistente de Importa&#231;&#227;o e Exporta&#231;&#227;o do SQL Server)
  Se você tiver selecionado um destino de arquivo simples, o Assistente de Importação e Exportação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] mostrará **Configurar Destino do Arquivo Simples** depois de especificar uma tabela a ser copiada ou depois de fornecer uma consulta. Nessa página, especifique opções de formatação para o arquivo simples de destino. Outra opção é examinar o mapeamento de colunas individuais e visualizar dados de exemplo.  
  
## <a name="screen-shot-of-the-configure-flat-file-destination-page"></a>Captura de tela da página Configurar Destino do Arquivo Simples  
 A captura de tela a seguir mostra a página **Configurar Destino do Arquivo Simples** do Assistente.
 
 Neste exemplo, o usuário deseja criar um arquivo CSV (valores separador por vírgula), isto é, terminar cada linha de dados na saída com uma combinação de retorno de carro e de alimentação de linha, além de separar as colunas de dados em cada linha com uma vírgula.

 ![Configure flat file page of the Import and Export Wizard](../../integration-services/import-export-data/media/flat-file.png "Configure flat file page of the Import and Export Wizard")  
  
## <a name="pick-a-source-table"></a>Selecionar uma tabela de origem. 
 **Tabela ou exibição de origem**  
 Selecione a tabela ou a exibição de origem.  

## <a name="specify-the-row-and-column-delimiters"></a>Especificar os delimitadores de linha e de coluna
 **Delimitador de linha**  
 Selecione na lista de delimitadores para linhas. Não há nenhuma opção para especificar um delimitador de linha personalizado.  
  
|Value|Description|  
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
 Selecione na lista de delimitadores para colunas. Não há nenhuma opção para especificar um delimitador de coluna personalizado.  
  
|Value|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|Delimite as colunas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|Delimite colunas com um retorno de carro.|  
|**{LF}**|Delimite colunas com uma alimentação de linha.|  
|**Ponto e vírgula {;}**|Delimite colunas com um ponto-e-vírgula.|  
|**Dois-pontos {:}**|Delimite colunas com dois-pontos.|  
|**Vírgula {,}**|Delimite colunas com uma vírgula.|  
|**Tabulação {t}**|Delimite colunas com uma tabulação.|  
|**Barra vertical {&#124;}**|Delimite colunas com uma barra vertical.|  

## <a name="optionally-edit-column-mappings-and-preview-sample-data"></a>Editar os mapeamentos de colunas e visualizar os dados de exemplo como opção

**Editar mapeamentos**   
Opcionalmente, clique em **Editar mapeamentos** para exibir a caixa de diálogo **Mapeamentos de Coluna** para a tabela selecionada. Use a caixa de diálogo **Mapeamentos de Coluna** para fazer o seguinte.
-   Examine o mapeamento de colunas individuais entre a origem e o destino.
-   Copie apenas um subconjunto de colunas selecionando **ignore** para as colunas que você não deseja copiar.

Para obter mais informações, consulte [Mapeamentos de coluna](../../integration-services/import-export-data/column-mappings-sql-server-import-and-export-wizard.md).  

**Visualização**  
Opcionalmente, clique em **Visualização** para visualizar até 200 linhas de dados de exemplo na caixa de diálogo **Visualizar Dados**. Isso confirma se o assistente vai copiar os dados que você deseja copiar. Para obter mais informações, consulte [Visualizar dados](../../integration-services/import-export-data/preview-data-dialog-box-sql-server-import-and-export-wizard.md).  
  
Depois de visualizar os dados, é recomendável alterar as opções selecionadas nas páginas anteriores do assistente. Para executar essas alterações, retorne para a página **Configurar Destino do Arquivo Simples** e clique em **Voltar** para retornar às páginas anteriores, nas quais é possível alterar as seleções.  

## <a name="whats-next"></a>O que vem a seguir?  
 Depois de especificar as opções de formatação para o arquivo de destino simples, a próxima página é **Salvar e executar pacote**. Nesta página, especifique se deseja executar a operação imediatamente. Dependendo da sua configuração, você também poderá salvar o pacote do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] criado pelo assistente para personalizá-lo e reutilizá-lo posteriormente. Para obter mais informações, consulte [Salvar e Executar o Pacote](../../integration-services/import-export-data/save-and-run-package-sql-server-import-and-export-wizard.md).  
