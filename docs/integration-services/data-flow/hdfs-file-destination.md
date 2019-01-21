---
title: Destino de arquivo HDFS | Microsoft Docs
ms.custom: ''
ms.date: 01/09/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.ssis.designer.hdfsfiledest.f1
ms.assetid: 4338ce9f-c077-4301-aca5-47ed070ec94d
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: f18f6b0516ab9ae417251e49f5a3cf24fd2aa997
ms.sourcegitcommit: 1c01af5b02fe185fd60718cc289829426dc86eaa
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 01/10/2019
ms.locfileid: "54185002"
---
# <a name="hdfs-file-destination"></a>Destino de Arquivo HDFS
  O componente Destino de Arquivo HDFS permite que um pacote do SSIS grave dados de um arquivo HDFS. Os formatos de arquivo com suporte são Texto, Avro e ORC.  
  
 Para configurar o Destino de Arquivo HDFS, arraste e solte a Origem de Arquivo HDFS no designer de fluxo de dados e clique duas vezes no componente para abrir o editor.  
  
 ![Editor de Destino de Arquivo HDFS](../../integration-services/data-flow/media/hdfs-file-dest.png "Editor de Destino de Arquivo HDFS")  
  
## <a name="options"></a>Opções  
 Configure as seguintes opções na guia **Geral** da caixa de diálogo **Editor de Destino de Arquivo Hadoop** .  
  
|Campo|Descrição|  
|-----------|-----------------|  
|**Conexão do Hadoop**|Especifique um gerenciador de conexões do Hadoop existente ou crie um novo. Esse gerenciador de conexões indica onde os arquivos HDFS estão hospedados.|  
|**Caminho do Arquivo**|Especifique o nome do arquivo HDFS.|  
|**Formato do arquivo**|Especifique o formato do arquivo HDFS. As opções disponíveis são Texto, Avro e ORC.|  
|**Caractere delimitador de coluna**|Se você selecionar o formato Texto, especifique o caractere delimitador de coluna.|  
|**Nomes de coluna na primeira linha de dados**|Se você selecionar o formato Texto, indique se a primeira linha no arquivo conterá nomes de coluna.|  
  
 Depois de configurar essas opções, selecione a guia **Colunas** para mapear colunas de origem para colunas de destino no fluxo de dados.  

::: moniker range=">= sql-server-ver15"
## <a name="prerequisite-for-orc-format"></a>Pré-requisito para o formato ORC

Antes de usar o formato de arquivo ORC, instale o JRE (Java Runtime Environment) versão 1.7.51 ou superior para a plataforma adequada.

Há suporte tanto para o JRE Zulu quanto para o Oracle.
-   [Zulu JRE](https://www.azul.com/downloads/zulu/zulu-windows/)
-   [JRE Oracle](https://www.oracle.com/technetwork/java/javase/downloads/jre8-downloads-2133155.html)

### <a name="set-up-the-zulu-jre"></a>Configurar o JRE Zulu

1. Baixe e extraia o pacote zip de instalação do Zulu OpenJDK.

2.  No Prompt de Comando, execute `sysdm.cpl`.

3. Na guia **Avançado**, selecione **Variáveis de Ambiente**.

4. Na seção **Variáveis do sistema** seção, selecione **Novo**.

5. Insira `JAVA_HOME` para o **Nome da variável**.

6. Selecione **Procurar Diretório**, navegue até a pasta de instalação do Zulu OpenJDK e selecione a subpasta `jre`. Em seguida, selecione OK. O valor da variável é preenchido automaticamente.

7. Selecione **OK** para fechar a caixa de diálogo **Nova Variável do Sistema**.

8. Selecione **OK** para fechar a caixa de diálogo Variáveis de Ambiente.

### <a name="set-up-the-oracle-jre"></a>Configurar o JRE Oracle

1. Baixe e execute o instalador exe do JRE Oracle.

1. Siga as instruções do instalador para concluir a instalação.

::: moniker-end

## <a name="see-also"></a>Consulte Também  
 [Gerenciador de conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)   
 [Origem do arquivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)  
