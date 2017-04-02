---
title: "Editor do Gerenciador de Conex&#245;es de Cache | Microsoft Docs"
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
  - "sql13.dts.designer.cacheconnection.f1"
ms.assetid: 0d8f9324-0c35-4eea-b06d-da3cc2426d2c
caps.latest.revision: 27
author: "douglaslMS"
ms.author: "douglasl"
manager: "jhubbard"
caps.handback.revision: 27
---
# Editor do Gerenciador de Conex&#245;es de Cache
  O gerenciador de conexões de Cache lê um conjunto de dados de referência da transformação Cache ou de um arquivo cache (.caw) e salva os dados em um arquivo cache. Os dados sempre são armazenados na memória.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna.  
  
 A transformação Pesquisa realiza as pesquisas no conjunto de dados de referência.  
  
 A caixa de diálogo **Editor do Gerenciador de Conexões de Cache** inclui as seguintes guias:  
  
-   [Guia Geral](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md#generaltab)  
  
-   [Guia Colunas](../../../integration-services/data-flow/transformations/cache-connection-manager-editor.md#columnstab)  
  
 Para obter mais informações sobre o Gerenciador de Conexões de Cache, consulte [Cache Connection Manager](../../../integration-services/data-flow/transformations/cache-connection-manager.md).  
  
##  <a name="generaltab"></a> Guia Geral  
 Use a guia **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para indicar se é necessário ler o cache de um arquivo ou salvar o cache em um arquivo.  
  
### Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de cache no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../../includes/ssis-md.md)] .  
  
 **Description**  
 Descreva a conexão. Como prática recomendável, descreva a conexão de acordo com a sua finalidade para tornar os pacotes autodocumentados e facilitar a sua manutenção.  
  
 **Usar cache de arquivo.**  
 Indique se precisa usar um arquivo de cache.  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../../integration-services/security/access-to-files-used-by-packages.md).  
  
 Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
-   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache. Para obter mais informações, consulte [Cache Transform](../../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Ler os dados do arquivo de cache.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo do arquivo de cache.  
  
 **Procurar**  
 Localize o arquivo de cache.  
  
 **Atualizar metadados**  
 Exclua os metadados de colunas no gerenciador de conexões de Cache e popule novamente o gerenciador de conexões do Cache com matadados de colunas de um arquivo de cache selecionado.  
  
##  <a name="columnstab"></a> Guia Colunas  
 Use a guia **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para configurar as propriedades de cada coluna no cache.  
  
### Opções  
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
  
 **Comprimento**  
 Especifica o tipo de dados da coluna. Se aplicável ao tipo de dados, você pode atualizar o **Comprimento**.  
  
 **Precisão**  
 Especifica a precisão de alguns tipos de dados de coluna. A precisão é o número de dígitos em um número. Se aplicável ao tipo de dados, você pode atualizar a **Precisão**.  
  
 **Escala**  
 Especifica a escala de alguns tipos de dados de coluna. A escala é o número de dígitos à direita da casa decimal em um número. Se aplicável ao tipo de dados, você pode atualizar a **Escala**.  
  
 **Página de Código**  
 Especifica a página de código para o tipo de coluna. Se aplicável ao tipo de dados, você pode atualizar a **Página de Código**.  
  
## Consulte também  
 [Transformação Pesquisa](../../../integration-services/data-flow/transformations/lookup-transformation.md)  
  
  