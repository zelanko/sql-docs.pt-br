---
title: Destino de Arquivo Flexível | Microsoft Docs
ms.custom: ''
ms.date: 05/22/2019
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
f1_keywords:
- sql13.dts.designer.afpextfiledest.f1
- sql14.dts.designer.afpextfiledest.f1
author: janinezhang
ms.author: janinez
ms.openlocfilehash: a8200ed17e9581f0c39693ee7386f7f33c566265
ms.sourcegitcommit: 2efb0fa21ff8093384c1df21f0e8910db15ef931
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/18/2019
ms.locfileid: "68316622"
---
# <a name="flexible-file-destination"></a>Destino de Arquivo Flexível

[!INCLUDE[ssis-appliesto](../../includes/ssis-appliesto-ssvrpluslinux-asdb-asdw-xxx.md)]

O componente **Destino de Arquivo Flexível** permite que um pacote do SSIS grave dados em vários serviços de armazenamento compatíveis.

Os serviços de armazenamento compatíveis no momento são

- [Armazenamento de Blobs do Azure](https://azure.microsoft.com/services/storage/blobs/)
- [Azure Data Lake Storage Gen2](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-introduction)
   
Arraste e solte **Destino de Arquivo Flexível** no designer de fluxo de dados e clique duas vezes nele para ver o editor.
  
O **Destino de Arquivo Flexível** é um componente do [Feature Pack do SSIS (SQL Server Integration Services) para Azure](../../integration-services/azure-feature-pack-for-integration-services-ssis.md).  

As propriedades a seguir estão disponíveis no **Editor de Destino de Arquivo Flexível**.

- **Tipo de Arquivo do Gerenciador de Conexões:** especifica o tipo do gerenciador de conexões de origem. Em seguida, escolha um já existente do tipo especificado ou crie um novo.
- **Caminho da Pasta:** especifica o caminho da pasta de destino.
- **Nome de Arquivo:** especifica o nome do arquivo de destino.
- **Formato do Arquivo:** especifica o formato do arquivo de destino. Os formatos compatíveis são **Text**, **Avro**, **ORC** e **Parquet**.
- **Caractere delimitador de coluna:** especifica o caractere a ser usado como delimitador de coluna (delimitadores com vários caracteres não são compatíveis).
- **Primeira linha como nome da coluna:** especifica se é necessário gravar os nomes de coluna na primeira linha.
- **Compactar o arquivo:** especifica se é necessário compactar o arquivo.
- **Tipo de Compactação:** especifica o formato de compactação a ser usado. Os formatos compatíveis são **GZIP**, **DEFLATE**, **BZIP2**.
- **Nível de Compactação:** especifica o nível de compactação a ser usado.

As propriedades a seguir estão disponíveis no **Editor Avançado**.

- **rowDelimiter:** o caractere usado para separar linhas em um arquivo. É permitido somente um caractere. O valor **padrão** é \r\n.
- **escapeChar:** o caractere especial usado para escapar um delimitador de coluna no conteúdo do arquivo de entrada. Não é possível especificar escapeChar e quoteChar para uma tabela. É permitido somente um caractere. Sem valor padrão.
- **quoteChar:** o caractere usado para colocar um valor de cadeia de caracteres entre aspas. Os delimitadores de coluna e linha que ficam dentro dos caracteres de aspas seriam tratados como parte do valor da cadeia de caracteres. Essa propriedade se aplica aos conjuntos de dados de entrada e de saída. Não é possível especificar escapeChar e quoteChar para uma tabela. É permitido somente um caractere. Sem valor padrão.
- **nullValue:** um ou mais caracteres usados para representar um valor nulo. O valor **padrão** é \N.
- **encodingName:** especifica o nome de codificação. Confira a propriedade [Encoding.EncodingName](https://docs.microsoft.com/dotnet/api/system.text.encoding?redirectedfrom=MSDN&view=netframework-4.8).
- **skipLineCount:**  indica o número de linhas não vazias a serem ignoradas ao ler dados dos arquivos de entrada. Se skipLineCount e firstRowAsHeader forem especificados, primeiro as linhas serão ignoradas e, em seguida, as informações de cabeçalho serão lidas no arquivo de entrada.
- **treatEmptyAsNull:** especifica se é necessário tratar uma cadeia de caracteres nula ou vazia como um valor nulo ao ler dados de um arquivo de entrada. O valor **padrão** é True.

Depois de especificar as informações de conexão, alterne para a página **Colunas** para mapear colunas de origem para colunas de destino para o fluxo de dados do SSIS.

**Observações sobre a configuração de permissão da entidade de serviço**

Para que a **conexão de teste** funcione (armazenamento de blobs ou Data Lake Storage Gen2), a entidade de serviço deve ser atribuída pelo menos à função de **Leitor de Dados do Storage Blob** para a conta de armazenamento.
Isso é feito com o [RBAC](https://docs.microsoft.com/azure/storage/common/storage-auth-aad-rbac-portal#assign-rbac-roles-using-the-azure-portal).

Para o armazenamento de blobs, a permissão de gravação é concedida por meio da atribuição de pelo menos a função de **Colaborador de dados do blob de armazenamento**.

Para o Azure Data Lake Storage Gen2, a permissão é determinada pelo RBAC e pelas [ACLs](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-how-to-set-permissions-storage-explorer).
Preste atenção nas ACLs que são configuradas usando a OID (ID de objeto) da entidade de serviço para o registro do aplicativo, conforme detalhado [aqui](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control#how-do-i-set-acls-correctly-for-a-service-principal).
Isso é diferente da ID do aplicativo (cliente) que é usada com a configuração de RBAC.
Quando uma entidade de segurança recebe permissões de dados RBAC por meio de uma função interna ou por meio de uma função personalizada, essas permissões são avaliadas primeiro após a autorização de uma solicitação.
Se a operação solicitada for autorizada pelas atribuições de RBAC da entidade de segurança, a autorização será imediatamente resolvida e nenhuma verificação de ACL adicional será executada.
Como alternativa, se a entidade de segurança não tiver uma atribuição de RBAC ou se a operação da solicitação não corresponder à permissão atribuída, as verificações de ACL serão executadas para determinar se a entidade de segurança está autorizada a executar a operação solicitada.
Para a permissão de gravação, conceda pelo menos a permissão de **execução** no sistema de arquivos do coletor, juntamente com a permissão de **gravação** para a pasta do coletor.
Como alternativa, conceda pelo menos a função de **Colaborador de dados do blob de armazenamento** com RBAC.
Consulte [este](https://docs.microsoft.com/azure/storage/blobs/data-lake-storage-access-control) artigo para obter detalhes.

**Pré-requisito para o Formato de Arquivo ORC/Parquet**

É necessário o Java para usar o formato de arquivo ORC/Parquet.
A arquitetura (32/64 bits) do build Java deve corresponder àquela do tempo de execução do SSIS para usar.
Os builds Java a seguir foram testados.

- [OpenJDK 8u192 do Zulu](https://www.azul.com/downloads/zulu/zulu-windows/)
- [Ambiente de Tempo de Execução Java do Oracle 8u192](https://www.oracle.com/technetwork/java/javase/downloads/java-archive-javase8-2177648.html)

**Configurar o OpenJDK do Zulu**

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

**Configurar o Ambiente de Tempo de Execução Java SE do Oracle**

1. Baixe e execute o instalador exe.
2. Siga as instruções do instalador para concluir a instalação.
