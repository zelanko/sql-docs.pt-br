---
title: Editor do Gerenciador de Conexão de cache | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology:
- integration-services
ms.topic: conceptual
f1_keywords:
- sql12.dts.designer.cacheconnection.f1
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: af7696c1d5194af721b6ff803736193db0285b8b
ms.sourcegitcommit: 5a8678bf85f65be590676745a7fe4fcbcc47e83d
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/22/2019
ms.locfileid: "58385044"
---
# <a name="cache-connection-manager-editor"></a>Editor do Gerenciador de Conexões de Cache
  O gerenciador de conexões de Cache lê um conjunto de dados de referência da transformação Cache ou de um arquivo cache (.caw) e salva os dados em um arquivo cache. Os dados sempre são armazenados na memória.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna.  
  
 A transformação Pesquisa realiza as pesquisas no conjunto de dados de referência.  
  
 A caixa de diálogo **Editor do Gerenciador de Conexões de Cache** inclui as seguintes guias:  
  
-   [Guia Geral](#generaltab)  
  
-   [Guia colunas](#columnstab)  
  
 Para obter mais informações sobre o Gerenciador de Conexões de Cache, consulte [Cache Connection Manager](connection-manager/cache-connection-manager.md).  
  
##  <a name="generaltab"></a> Guia Geral  
 Use a guia **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para indicar se é necessário ler o cache de um arquivo ou salvar o cache em um arquivo.  
  
### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de cache no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../includes/ssis-md.md)] .  
  
 **Descrição**  
 Descreva a conexão. Como prática recomendável, descreva a conexão de acordo com a sua finalidade para tornar os pacotes autodocumentados e facilitar a sua manutenção.  
  
 **Usar cache de arquivo.**  
 Indique se precisa usar um arquivo de cache.  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../2014/integration-services/access-to-files-used-by-packages.md).  
  
 Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
-   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache. Para obter mais informações, consulte [Cache Transform](data-flow/transformations/cache-transform.md).  
  
-   Ler os dados do arquivo de cache.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo do arquivo de cache.  
  
 **Procurar**  
 Localize o arquivo de cache.  
  
 **Atualizar metadados**  
 Exclua os metadados de colunas no gerenciador de conexões de Cache e popule novamente o gerenciador de conexões do Cache com matadados de colunas de um arquivo de cache selecionado.  
  
##  <a name="columnstab"></a> Guia Colunas  
 Use a guia **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para configurar as propriedades de cada coluna no cache.  
  
### <a name="options"></a>Opções  
 **Coluna**  
 Especifique o nome da coluna.  
  
 **Posição de Índice**  
 Especifique quais colunas são colunas de índice indicando a posição de índice de cada coluna. O índice é uma coleção de uma ou mais colunas.  
  
 Para colunas sem-índice, a posição de índice é 0.  
  
 Para colunas de índice, a posição de índice é um número sequencial positivo. Este número indica a ordem na qual a transformação Pesquisa compara as linhas no conjunto de dados de referência às linhas na fonte de dados de entrada. A coluna com os valores mais exclusivos deve ter a posição de índice mais baixa.  
  
> [!NOTE]  
>  Quando a transformação Pesquisa é configurada para usar um gerenciador de conexões de Cache, somente as colunas de índice no conjunto de dados de referência podem ser mapeadas para as colunas de entrada. Além disso, todas as colunas de índice devem ser mapeadas.  
  
 **Tipo**  
 Especifique o tipo de dados da coluna  
  
 `Length`  
 Especifica o tipo de dados da coluna. Se aplicável ao tipo de dados, você pode atualizar a `Length`.  
  
 `Precision`  
 Especifica a precisão de alguns tipos de dados de coluna. A precisão é o número de dígitos em um número. Se aplicável ao tipo de dados, você pode atualizar a `Precision`.  
  
 `Scale`  
 Especifica a escala de alguns tipos de dados de coluna. A escala é o número de dígitos à direita da casa decimal em um número. Se aplicável ao tipo de dados, você pode atualizar a `Scale`.  
  
 `Code Page`  
 Especifica a página de código para o tipo de coluna. Se aplicável ao tipo de dados, você pode atualizar a `Code Page`.  
  
## <a name="see-also"></a>Consulte também  
 [Lookup Transformation](data-flow/transformations/lookup-transformation.md)  
  
  
