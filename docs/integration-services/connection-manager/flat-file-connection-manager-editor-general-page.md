---
title: "Editor do Gerenciador de Conex&#245;es de Arquivos Simples (p&#225;gina Geral) | Microsoft Docs"
ms.custom: ""
ms.date: "03/01/2017"
ms.prod: "sql-server-2016"
ms.reviewer: ""
ms.suite: ""
ms.technology: 
  - "integration-services"
ms.tgt_pltfrm: ""
ms.topic: "article"
f1_keywords: 
  - "sql13.dts.designer.ffileconnection.general.f1"
helpviewer_keywords: 
  - "Editor do Gerenciador de Conexões de Arquivos Simples"
ms.assetid: 77296024-5c1a-4f6a-9665-0b50d45d744c
caps.latest.revision: 24
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 24
---
# Editor do Gerenciador de Conex&#245;es de Arquivos Simples (p&#225;gina Geral)
  Use a página **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Arquivos Simples** para selecionar um arquivo e formato de dados. Uma conexão de arquivos simples habilita um pacote a conectar-se com um arquivo de texto.  
  
 Para obter mais informações sobre o gerenciador de conexões de Arquivo Simples, consulte [Flat File Connection Manager](../../integration-services/connection-manager/flat-file-connection-manager.md).  
  
## Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de arquivos simples no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
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
  
|Value|Description|  
|-----------|-----------------|  
|Delimitado|As colunas são separadas por delimitadores, especificados na página **Colunas** .|  
|Largura fixa|As colunas têm uma largura fixa.|  
|Irregular à direita|Arquivos irregulares à direita são arquivos em que toda coluna tem uma largura fixa, à exceção da última coluna. Ela é delimitada pelo delimitador de linha.|  
  
 **Qualificador de texto**  
 Especifique o qualificador de texto a ser usado. Por exemplo, você pode especificar que os campos de texto fiquem entre aspas.  
  
> [!NOTE]  
>  Depois de selecionar um qualificador de texto, você não pode selecionar a opção **None**. Digite **None** para anular a seleção do qualificador de texto.  
  
 **Delimitador de linha de cabeçalho**  
 Selecione na lista de delimitadores de linhas de cabeçalho ou digite o texto do delimitador.  
  
|Value|Description|  
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
  
## Consulte também  
 [Referência de mensagens e erros do Integration Services](../../integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Colunas&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-columns-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Avançado&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-advanced-page.md)   
 [Editor do Gerenciador de Conexões de Arquivos Simples &#40;Página Visualização&#41;](../../integration-services/connection-manager/flat-file-connection-manager-editor-preview-page.md)  
  
  