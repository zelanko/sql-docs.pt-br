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
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 418921c7ce0f37cbbf7953f6b8023a717f8ae54b
ms.sourcegitcommit: 3026c22b7fba19059a769ea5f367c4f51efaf286
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/15/2019
ms.locfileid: "65726777"
---
# <a name="hdfs-file-destination"></a>Destino de Arquivo HDFS

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]


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

## <a name="prerequisite-for-orc-file-format"></a>Pré-requisito para o Formato de Arquivo ORC
Java é necessário para usar o formato de arquivo ORC.
A arquitetura (32/64 bits) do build Java deve corresponder àquela do tempo de execução do SSIS para usar.
Os builds Java a seguir foram testados.

- [OpenJDK 8u192 do Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Ambiente de Tempo de Execução Java do Oracle 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

### <a name="set-up-zulus-openjdk"></a>Configurar o OpenJDK do Zulu
1. Baixe e extraia o pacote de instalação zip.
2. No Prompt de Comando, execute `sysdm.cpl`.
3. Na guia **Avançado**, selecione **Variáveis de Ambiente**.
4. Na seção **Variáveis do sistema** seção, selecione **Novo**.
5. Insira `JAVA_HOME` para o **Nome da variável**.
6. Selecione **Procurar Diretório**, navegue até a pasta extraída e selecione a subpasta `jre`.
   Em seguida, selecione **OK** e o **Valor da variável** será preenchido automaticamente.
7. Selecione **OK** para fechar a caixa de diálogo **Nova Variável do Sistema**.
8. Selecione **OK** para fechar a caixa de diálogo **Variáveis de Ambiente**.
9. Selecione **OK** para fechar a caixa de diálogo **Propriedades do Sistema**.

### <a name="set-up-oracles-java-se-runtime-environment"></a>Configurar o Ambiente de Tempo de Execução Java SE do Oracle
1. Baixe e execute o instalador exe.
2. Siga as instruções do instalador para concluir a instalação.

::: moniker-end

## <a name="see-also"></a>Consulte Também
[Gerenciador de Conexões do Hadoop](../../integration-services/connection-manager/hadoop-connection-manager.md)  
[Origem de arquivo HDFS](../../integration-services/data-flow/hdfs-file-source.md)
