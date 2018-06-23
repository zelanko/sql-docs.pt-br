---
title: Editor do Gerenciador de Conexão de arquivo (página geral) simples | Microsoft Docs
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
- sql12.dts.designer.ffileconnection.general.f1
helpviewer_keywords:
- Flat File Connection Manager Editor
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.openlocfilehash: 5109aee94d7f566da2f3cf3d61b1a9569d6a44e0
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36115478"
---
# <a name="flat-file-connection-manager-editor-general-page"></a>Editor do Gerenciador de Conexões de Arquivos Simples (página Geral)
  Use a página **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para selecionar um arquivo e formato de dados. Uma conexão de arquivos simples habilita um pacote a conectar-se com um arquivo de texto.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](connection-manager/file-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de arquivos simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo a ser usado na conexão de arquivos simples.  
  
 **Procurar**  
 Localize o nome do arquivo a ser usado na conexão de arquivos simples.  
  
 **Localidade**  
 Especifique a localidade para fornecer informações de idioma específicas para solicitações e formatos de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. Se você usar o Unicode, não poderá especificar uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formato**  
 Indique se o arquivo usa formatação delimitada, de largura fixa ou irregular à direita.  
  
|Valor|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores, especificados na página **Colunas** .|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto a ser usado. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas.  
  
> [!NOTE]  
>  Depois de selecionar um qualificador de texto, você não pode selecionar a opção **None** . Digite **None** para anular a seleção do qualificador de texto.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Valor|Description|  
|-----------|-----------------|  
|**{CR}{LF}**|A linha do cabeçalho é delimitada por uma combinação de retorno de carro e avanço de linha.|  
|**{CR}**|A linha do cabeçalho é delimitada por um retorno de carro.|  
|**{LF}**|A linha do cabeçalho é delimitada por um avanço de linha.|  
|**Ponto-e-vírgula {;}**|A linha do cabeçalho é delimitada por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|A linha do cabeçalho é delimitada por dois-pontos.|  
|**Vírgula {,}**|A linha do cabeçalho é delimitada por uma vírgula.|  
|**Tabulação {t}**|A linha do cabeçalho é delimitada por uma tabulação.|  
|**Barra vertical {&#124;}**|A linha do cabeçalho é delimitada por uma barra vertical.|  
  
 **Linhas de cabeçalho a ignorar**  
 Especifique o número de linhas de cabeçalho ou linhas de dados iniciais a ignorar, caso existam.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se deseja esperar ou fornecer nomes de coluna na primeira linha de dados.  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexão de arquivo simples &#40;página colunas&#41;](../../2014/integration-services/flat-file-connection-manager-editor-columns-page.md)   
 [Editor do Gerenciador de Conexão de arquivo simples &#40;página Avançado&#41;](../../2014/integration-services/flat-file-connection-manager-editor-advanced-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/flat-file-connection-manager-editor-preview-page.md)  
  
  