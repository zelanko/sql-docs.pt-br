---
title: Vários arquivos simples Editor do Gerenciador de Conexão (página Avançado) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.multifile.advanced.f1
helpviewer_keywords:
- Multiple Flat Files Connection Manager Editor
ms.assetid: fc883131-c03d-4ab3-8220-b51cbe243a82
author: douglaslms
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 83e6aae7d4383440f148a8de1480cb8f1658e89c
ms.sourcegitcommit: 2429fbcdb751211313bd655a4825ffb33354bda3
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/28/2018
ms.locfileid: "52542741"
---
# <a name="multiple-flat-files-connection-manager-editor-advanced-page"></a>Editor do Gerenciador de Conexões de Vários Arquivos Simples (Página Avançado)
  Use a página **Avançado** da caixa de diálogo **Editor do Gerenciador de Conexões de Vários Arquivos Simples** para definir propriedades como o tipo de dados e os delimitadores de cada coluna nos arquivos de texto com os quais o gerenciador de conexões de arquivos simples se conecta.  
  
 Por padrão, o tamanho da coluna de cadeia de caracteres é de 50 caracteres. É possível avaliar os dados de exemplo e automaticamente redimensionar o tamanho dessas colunas para impedir o truncamento de dados ou excesso de largura das colunas. Também é possível atualizar outros metadados para habilitar a compatibilidade com as colunas de destino. Por exemplo, você pode alterar o tipo de dados de uma coluna que contém apenas dados inteiros para um tipo de dados numérico, como DT_I2.  
  
 Para saber mais sobre o gerenciador de conexões de Vários Arquivos Simples, consulte [Multiple Flat Files Connection Manager](connection-manager/multiple-flat-files-connection-manager.md).  
  
## <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para o gerenciador de conexões de Vários Arquivos Simples no fluxo de trabalho. O nome fornecido será exibido na área **Gerenciadores de Conexões** do Designer [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva o gerenciador de conexões. Como prática recomendável, descreva o gerenciador de conexões em termos de objetivo, para tornar os pacotes autodocumentados e mais fáceis de manter.  
  
 **Configurar as propriedades de cada coluna**  
 Selecione uma coluna no painel esquerdo para exibir suas propriedades no painel direito. Consulte a tabela a seguir para obter uma descrição das propriedades dos tipos de dados. Algumas das propriedades listadas são configuráveis apenas para alguns formatos de arquivo simples.  
  
|Propriedade|Descrição|  
|--------------|-----------------|  
|**ColumnType**|Denota se a coluna é delimitada, de largura fixa ou com imperfeição à direita. Esta propriedade é somente leitura. Nos arquivos irregulares à direita, todas as colunas têm uma largura fixa, com exceção da última, que é encerrada pelo delimitador de linha.|  
|**OutputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Na tarefa Fluxo de Dados, esse valor é usado para definir a largura de coluna de saída para a fonte de Arquivo Simples.<br /><br /> Observação: No modelo de objeto, o nome desta propriedade é MaximumWidth.|  
|**DataType**|Seleciona na lista de tipos de dados disponíveis. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**TextQualified**|Indica se os dados de texto são qualificados usando um caractere de qualificador de texto. Os valores válidos são:<br /><br /> **True**: Os dados de texto no arquivo simples são qualificados.<br /><br /> **False**: Os dados de texto no arquivo simples não são qualificados.|  
|**Nome**|Forneça um nome de coluna. O padrão é uma lista numerada das colunas; entretanto, é possível escolher qualquer nome exclusivo e descritivo.|  
|**DataScale**|Especifica a escala de dados numéricos. A escala se refere ao número de casas decimais. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**ColumnDelimiter**|Seleciona na lista de delimitadores de coluna disponíveis. Escolha delimitadores com pouca probabilidade de ocorrer no texto. Esse valor é ignorado para colunas de largura fixa.<br /><br /> **{CR}{LF}** – as colunas são delimitadas por uma combinação de retorno de carro e de alimentação de linha<br /><br /> **{CR}** – as colunas são delimitadas por um retorno de carro<br /><br /> **{LF}** – as colunas são delimitadas por uma alimentação de linha<br /><br /> **Ponto e vírgula {;}** – as colunas são delimitadas por um ponto e vírgula<br /><br /> **Dois pontos {:}** – as colunas são delimitadas por dois pontos<br /><br /> **Vírgula {,}** – as colunas são delimitadas por uma vírgula<br /><br /> **Tabulação {t}** – as colunas são delimitadas por uma tabulação<br /><br /> **Barra vertical {&#124;}** – as colunas são delimitadas por uma barra vertical|  
|**DataPrecision**|Especifica a precisão de dados numéricos. A precisão se refere ao número de dígitos. Para obter mais informações, consulte [Integration Services Data Types](data-flow/integration-services-data-types.md).|  
|**InputColumnWidth**|Especifica um valor a ser armazenado como contagem de bytes; no caso de arquivos Unicode, isso será exibido como contagem de caracteres. Este valor é ignorado nas colunas delimitadas.<br /><br /> **Observação** No modelo de objeto, o nome desta propriedade é ColumnWidth.|  
  
 **Nova**  
 Adicione uma nova coluna, clicando em **Nova**. Por padrão, o botão **Nova** adiciona uma nova coluna ao final da lista. O botão também tem as opções a seguir, disponíveis na lista suspensa.  
  
|Valor|Descrição|  
|-----------|-----------------|  
|**Adicionar Coluna**|Adiciona uma nova coluna fim da lista.|  
|**Insert Before**|Insere uma nova coluna antes da coluna selecionada.|  
|**Insert After**|Insere uma nova coluna depois da coluna selecionada.|  
  
 **Delete (excluir)**  
 Selecione uma coluna e remova-a, clicando em **Excluir**.  
  
 **Sugerir Tipos**  
 Use a caixa de diálogo **Sugerir Tipos de Coluna** para avaliar dados de exemplo no primeiro arquivo selecionado e obter sugestões de tipo de dados e tamanho de cada coluna. Para obter mais informações, consulte [Referência da interface do usuário da caixa de diálogo Sugerir Tipos de Coluna](connection-manager/suggest-column-types-dialog-box-ui-reference.md).  
  
## <a name="see-also"></a>Consulte também  
 [Referência de mensagens e erros do Integration Services](../../2014/integration-services/integration-services-error-and-message-reference.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Geral&#41;](general-page-of-integration-services-designers-options.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Colunas&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-columns-page.md)   
 [Editor do Gerenciador de Conexões de Vários Arquivos Simples &#40;Página Visualização&#41;](../../2014/integration-services/multiple-flat-files-connection-manager-editor-preview-page.md)  
  
  
