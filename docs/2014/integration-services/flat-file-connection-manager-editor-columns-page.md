---
title: Editor do Gerenciador de Conexão de arquivo (página colunas) simples | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- integration-services
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.dts.designer.ffileconnection.columns.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 40ce7537-abd0-4973-97fd-6ccb90fddfa0
caps.latest.revision: 20
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5592f71b5373c6bfab1f59e797b19363a344e929
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36012294"
---
# <a name="flat-file-connection-manager-editor-columns-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Colunas)
  Use a página **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para especificar a linha e informações da coluna, e visualizar o arquivo.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Arquivo Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
## <a name="flat-file-format-dynamic-options"></a>Opções dinâmicas do formato de arquivo simples  
  
### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As linhas são delimitadas por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|As linhas são delimitadas por um retorno de carro.|  
|**{LF}**|As linhas são delimitadas por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|As linhas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As linhas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As linhas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As linhas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As linhas são delimitadas por uma barra vertical.|  
  
 **Delimitador de coluna**  
 Selecione na lista de delimitadores de coluna disponíveis ou digite o texto delimitador.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Atualizar**  
 Exiba o efeito de alterar os delimitadores a serem ignorados clicando em **Atualizar**. Esse botão só ficará visível após você alterar outras opções de conexão.  
  
 **Visualizar linhas**  
 Exiba os dados de amostra do arquivo simples, dividido em colunas e linhas, usando as opções selecionadas.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
### <a name="format--fixed-width"></a>Formato = Largura fixa  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vermelha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
### <a name="format--ragged-right"></a>Formato = Irregular à direita  
  
> [!NOTE]  
>  Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.  
  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical vermelho e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|As linhas são delimitadas por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|As linhas são delimitadas por um retorno de carro.|  
|**{LF}**|As linhas são delimitadas por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|As linhas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As linhas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As linhas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As linhas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As linhas são delimitadas por uma barra vertical.|  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexão de arquivo simples &#40;página geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor do Gerenciador de Conexão de arquivo simples &#40;página Avançado&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  