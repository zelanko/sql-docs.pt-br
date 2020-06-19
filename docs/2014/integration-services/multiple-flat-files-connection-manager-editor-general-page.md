---
title: Editor do Gerenciador de conexões de vários arquivos simples (página Geral) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.general.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: 00129d43-2772-413b-bdf8-ac5de81cf4a5
author: janinezhang
ms.author: janinez
ms.openlocfilehash: 11c56c29f685eb8f3746431a79b4d6a42a4b9fe5
ms.sourcegitcommit: f71e523da72019de81a8bd5a0394a62f7f76ea20
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84965136"
---
# <a name="multiple-flat-files-connection-manager-editor-general-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (página Geral)
  Use a página **Geral** da caixa de diálogo do **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para selecionar um grupo de arquivos que têm o mesmo formato de dados e para especificar seu formato de dados. Uma conexão de vários arquivos simples habilita um pacote a conectar-se com um grupo de arquivos de texto que têm o mesmo formato.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Nome do Gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Nomes de arquivo**  
 Digite o caminho e o nome de arquivos para usar na conexão de vários arquivos simples. Você pode especificar vários arquivos usando curingas, como no exemplo “C:\\*.txt”, ou usando o caractere de barra vertical (|) para separar vários nomes de arquivo. Todos os arquivos devem ter o mesmo formato de dados.  
  
 **Procurar**  
 Procure os nomes de arquivo para usar na conexão de vários arquivos simples. Você pode selecionar vários arquivos. Todos os arquivos devem ter o mesmo formato de dados.  
  
 **Local**  
 Especifique a localidade para fornecer informações de classificação e de conversão de data e hora.  
  
 **Unicode**  
 Indique se deve ser usado o Unicode. O uso do Unicode impede a especificação de uma página de código.  
  
 **Página de código**  
 Especifique a página de código do texto não Unicode.  
  
 **Formatar**  
 Indique se será usada formatação delimitada, de largura fixa ou irregular à direita. Todos os arquivos devem ter o mesmo formato de dados.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores, especificados na página **Colunas** .|  
|Largura fixa|As colunas têm uma largura fixa, especificada arrastando as linhas do marcador na página **Colunas** .|  
|Irregular à direita|Em arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é delimitada pelo delimitador de linha especificado na página **Colunas** .|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto a ser usado. Por exemplo, você pode especificar incluir o texto entre aspas.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**{CR}{LF}**|A linha do cabeçalho é delimitada por uma combinação de retorno de carro e avanço de linha.|  
|**CD**|A linha do cabeçalho é delimitada por um retorno de carro.|  
|**{LF}**|A linha do cabeçalho é delimitada por um avanço de linha.|  
|**Ponto e vírgula {;}**|A linha do cabeçalho é delimitada por um ponto-e-vírgula.|  
|**Dois-pontos {:}**|A linha do cabeçalho é delimitada por dois-pontos.|  
|**Pontos{,}**|A linha do cabeçalho é delimitada por uma vírgula.|  
|**Tabulação {t}**|A linha do cabeçalho é delimitada por uma tabulação.|  
|**Barra vertical {&#124;}**|A linha do cabeçalho é delimitada por uma barra vertical.|  
  
 **Linhas de cabeçalho a ignorar**  
 Especifique o número de linhas de cabeçalho a ignorar, caso existam.  
  
 **Nomes de coluna na primeira linha de dados**  
 Indique se deseja esperar ou fornecer nomes de coluna na primeira linha de dados.  
  
## <a name="see-also"></a>Consulte Também  
 [Integration Services referência de erro e mensagem](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de conexões de vários arquivos simples &#40;página colunas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor do Gerenciador de conexões de vários arquivos simples &#40;página avançado&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-advanced-page.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
