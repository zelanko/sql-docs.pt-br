---
title: Gerenciador de Conexões do Cache | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- Cache connection manager
ms.assetid: bdc92038-3720-4795-8a5c-79b963f2c952
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1026f4c20042a9aec24256238190dd1a230bda42
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "62833586"
---
# <a name="cache-connection-manager"></a>Gerenciador de conexões do cache
  O gerenciador de conexões do Cache lê dados da transformação Cache ou de um arquivo de cache (.caw) e salva os dados em um arquivo de cache. Se você configurar o gerenciador de conexões do Cache para usar um arquivo de cache, os dados sempre serão armazenados na memória.  
  
 A transformação Cache grava dados de uma fonte de dados conectada no fluxo de dados para um gerenciador de conexões do Cache. A transformação Pesquisa em um pacote realiza pesquisas nos dados.  
  
> [!NOTE]  
>  O gerenciador de conexões do Cache não oferece suporte aos tipos de dados BLOB (objetos binários grandes) DT_TEXT, DT_NTEXT e DT_IMAGE. Se o conjunto de dados de referência contiver um tipo de dados BLOB, o componente irá falhar quando o pacote for executado. Você pode usar o **Editor do Gerenciador de Conexões de Cache** para modificar os tipos de dados da coluna. Para obter mais informações, consulte [Cache Connection Manager Editor](../cache-connection-manager-editor.md).  
  
> [!NOTE]  
>  O nível de proteção do pacote não se aplica ao arquivo de cache. Se o arquivo de cache tiver informações confidenciais, use uma lista de controle de acesso (ACL) para restringir o acesso ao local ou à pasta na qual você deseja armazenar o arquivo. Você deve habilitar o acesso apenas para determinadas contas. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
## <a name="configuration-of-the-cache-connection-manager"></a>Configuração do gerenciador de conexões do Cache  
 Você pode configurar o gerenciador de conexões do Cache das seguintes maneiras:  
  
-   Indique se precisa usar um arquivo de cache.  
  
     Se você configurar o gerenciador de conexões de cache para usar um arquivo de cache, o gerenciador irá realizar uma das seguintes ações:  
  
    -   Salvar os dados no arquivo quando a transformação Cache estiver configurada para gravar dados de uma fonte de dados no fluxo de dados para o gerenciador de conexões de cache.  
  
    -   Ler os dados do arquivo de cache.  
  
     Para obter mais informações, consulte [Cache Transform](../data-flow/transformations/cache-transform.md).  
  
-   Altere os metadados para as colunas armazenadas no cache.  
  
-   Atualize o nome do arquivo de cache no runtime usando uma expressão para definir a propriedade ConnectionString. Para obter mais informações, consulte [Usar expressões de propriedade em pacotes](../expressions/use-property-expressions-in-packages.md).  
  
 Você pode definir propriedades pelo Designer do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] ou programaticamente.  
  
 Para obter mais informações sobre as propriedades que podem ser definidas no Designer do [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] , consulte [Editor do Gerenciador de Conexões de Cache](../cache-connection-manager-editor.md).  
  
 Para obter informações sobre como configurar um gerenciador de conexões de forma programática, consulte <xref:Microsoft.SqlServer.Dts.Runtime.ConnectionManager> e [Adicionar conexões programaticamente](../building-packages-programmatically/adding-connections-programmatically.md).  
  
## <a name="related-tasks"></a>Related Tasks  
 [Implementar uma Transformação de Pesquisa em modo de Cache Cheio usando o Gerenciador de Conexões de Cache](lookup-transformation-full-cache-mode-ole-db-connection-manager.md)  
  
  
