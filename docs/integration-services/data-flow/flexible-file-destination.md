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
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 9bb840838794d7fc5a2e67acc7a4a2438ea2faf1
ms.sourcegitcommit: e8af8cfc0bb51f62a4f0fa794c784f1aed006c71
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 09/26/2019
ms.locfileid: "71292452"
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
- **Formato do Arquivo:** especifica o formato do arquivo de destino. Os formatos compatíveis são **Text**, **Avro**, **ORC** e **Parquet**. É necessário ter Java para ORC/Paquet. Confira [aqui](../../integration-services/azure-feature-pack-for-integration-services-ssis.md#dependency-on-java) para obter detalhes.
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