---
title: "Gerenciador de Conexão de cache | Microsoft Docs"
ms.custom: 
ms.date: 03/07/2017
ms.prod: sql-non-specified
ms.prod_service: integration-services
ms.service: 
ms.component: connection-manager
ms.reviewer: 
ms.suite: sql
ms.technology:
- integration-services
ms.tgt_pltfrm: 
ms.topic: article
f1_keywords:
- sql13.dts.designer.cacheconnection.f1
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
caps.latest.revision: 23
author: douglaslMS
ms.author: douglasl
manager: jhubbard
ms.workload: Inactive
ms.translationtype: MT
ms.sourcegitcommit: 8397673c7ed9dfe8ae02871f9077ed7286e49863
ms.openlocfilehash: 481075f02dff2f4900eeca549835b990b50aee37
ms.contentlocale: pt-br
ms.lasthandoff: 08/09/2017

---
# <a name="cache-connection-manager"></a>Gerenciador de conexões do cache
  O gerenciador de conexões do Cache lê dados da transformação Cache ou de um arquivo de cache (.caw) e salva os dados em um arquivo de cache. Se você configurar o gerenciador de conexões do Cache para usar um arquivo de cache, os dados sempre serão armazenados na memória.  
  
 A transformação Cache grava dados de uma fonte de dados conectada no fluxo de dados para um gerenciador de conexões do Cache. A transformação Pesquisa em um pacote realiza pesquisas nos dados.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna. Para obter mais informações, consulte [Cache Connection Manager Editor](cache-connection-manager-editor.md).  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
  
## <a name="configuration-of-the-cache-connection-manager"></a>Configuração do gerenciador de conexões do Cache  
 Você pode configurar o gerenciador de conexões do Cache das seguintes maneiras:  
  
-   Indique se precisa usar um arquivo de cache.  
  
     Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
    -   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache.  
  
    -   Ler os dados do arquivo de cache.  
  
     Para obter mais informações, consulte [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Altere os metadados para as colunas armazenadas no cache.  
  
-   Atualize o nome do arquivo de cache no tempo de execução usando uma expressão para definir a propriedade ConnectionString. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../../integration-services/expressions/use-property-expressions-in-packages.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou programaticamente.  
  
 Para obter informações sobre como configurar um Gerenciador de conexão de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [adicionando conexões programaticamente](../../integration-services/building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="cache-connection-manager-editor"></a>Editor do Gerenciador de Conexões de Cache
  O gerenciador de conexões de Cache lê um conjunto de dados de referência da transformação Cache ou de um arquivo cache (.caw) e salva os dados em um arquivo cache. Os dados sempre são armazenados na memória.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna.  
  
 A transformação Pesquisa realiza as pesquisas no conjunto de dados de referência.  
  
 A caixa de diálogo **Editor do Gerenciador de Conexões de Cache** inclui as seguintes guias:  
  
###  <a name="generaltab"></a> Guia Geral  
 Use a guia **Geral** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para indicar se é necessário ler o cache de um arquivo ou salvar o cache em um arquivo.  
  
#### <a name="options"></a>Opções  
 **Nome do gerenciador de conexões**  
 Forneça um nome exclusivo para a conexão de cache no fluxo de trabalho. O nome fornecido será exibido no Designer do [!INCLUDE[ssIS](../../includes/ssis-md.md)] .  
  
 **Description**  
 Descreva a conexão. Como prática recomendável, descreva a conexão de acordo com a sua finalidade para tornar os pacotes autodocumentados e facilitar a sua manutenção.  
  
 **Usar cache de arquivo.**  
 Indique se precisa usar um arquivo de cache.  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../../integration-services/security/security-overview-integration-services.md#files).  
  
 Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
-   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache. Para obter mais informações, consulte [Cache Transform](../../integration-services/data-flow/transformations/cache-transform.md).  
  
-   Ler os dados do arquivo de cache.  
  
 **Nome do arquivo**  
 Digite o caminho e o nome do arquivo do arquivo de cache.  
  
 **Procurar**  
 Localize o arquivo de cache.  
  
 **Atualizar metadados**  
 Exclua os metadados de colunas no gerenciador de conexões de Cache e popule novamente o gerenciador de conexões do Cache com matadados de colunas de um arquivo de cache selecionado.  
  
###  <a name="columnstab"></a> Guia Colunas  
 Use a guia **Colunas** da caixa de diálogo **Editor do Gerenciador de Conexões de Cache** para configurar as propriedades de cada coluna no cache.  
  
#### <a name="options"></a>Opções  
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
  
## <a name="related-tasks"></a>Tarefas relacionadas  
 [Implementar uma transformação pesquisa em modo de Cache cheio usando o Gerenciador de Conexão de Cache](lookup-transformation-full-cache-mode-cache-connection-manager.md)  
  
  

