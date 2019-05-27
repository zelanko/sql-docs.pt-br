---
title: Vários arquivos simples (página colunas) de Editor do Gerenciador de Conexão | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.columns.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: ad0cb668-0df2-4d4e-9a20-d20692a0b67a
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: b44fe16f89e154c1008c73400a6815e9e548bb69
ms.sourcegitcommit: f40fa47619512a9a9c3e3258fda3242c76c008e6
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 05/23/2019
ms.locfileid: "66057495"
---
# <a name="multiple-flat-files-connection-manager-editor-columns-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (página Colunas)
  Use o nó **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para especificar as informações da linha e da coluna e visualizar o primeiro arquivo selecionado.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="static-options"></a>Opções estáticas  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
## <a name="flat-file-format-dynamic-options"></a>Opções dinâmicas do formato de arquivo simples  
  
### <a name="format--delimited"></a>Formato = Delimitado  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Descrição|  
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
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|As colunas são delimitadas por uma combinação de retorno de carro e alimentação de linha.|  
|**{CR}**|As colunas são delimitadas por um retorno de carro.|  
|**{LF}**|As colunas são delimitadas por uma alimentação de linha.|  
|**Ponto-e-vírgula {;}**|As colunas são delimitadas por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|As colunas são delimitadas por dois-pontos.|  
|**Vírgula {,}**|As colunas são delimitadas por uma vírgula.|  
|**Tabulação {t}**|As colunas são delimitadas por uma tabulação.|  
|**Barra vertical {&#124;}**|As colunas são delimitadas por uma barra vertical.|  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
### <a name="format--fixed-width"></a>Formato = Largura fixa  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Largura da linha**  
 Especifique o comprimento da linha antes de adicionar delimitadores para colunas individuais. Você também pode arrastar a linha vertical na janela de visualização para marcar o fim da linha. O valor de largura da linha é atualizado automaticamente.  
  
 **Redefinir Colunas**  
 Remova todas as colunas, exceto as originais, clicando em **Redefinir Colunas**.  
  
### <a name="format--ragged-right"></a>Formato = Irregular à direita  
  
> [!NOTE]  
>  Arquivos irregulares à direita são arquivos nos quais toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.  
  
 **Fonte**  
 Selecione a fonte em que os dados de visualização serão exibidos.  
  
 **Colunas de dados de origem**  
 Ajuste a largura da linha deslizando o marcador de linha vertical e ajuste a largura das colunas clicando na régua na parte superior da janela de visualização  
  
 **Delimitador de linha**  
 Selecione na lista de delimitadores de linha disponíveis ou digite o texto delimitador.  
  
|Valor|Descrição|  
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
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Avançado&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
