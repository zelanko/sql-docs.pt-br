---
title: Contêineres de Clusters de Big Data não raiz
titleSuffix: SQL Server big data clusters
description: Este artigo descreve como implantar contêineres não raiz em Clusters de Big Data do SQL Server
author: mihaelablendea
ms.author: mihaelab
ms.reviewer: mikeray
ms.date: 06/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e74e08146ea4c92f23ba17816738122147150e7b
ms.sourcegitcommit: ae474d21db4f724523e419622ce79f611e956a22
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/20/2020
ms.locfileid: "92257116"
---
# <a name="non-root-big-data-clusters-containers"></a>Contêineres de Clusters de Big Data não raiz

O SQL Server 2019 CU5 introduz o suporte para contêineres não raiz. A implementação da plataforma é mais segura verificando se todos os aplicativos de contêiner em execução no BDC são iniciados como usuários não raiz por padrão, em todas as plataformas com suporte. Essas funcionalidades estão disponíveis para todas as novas implantações usando a marca de imagem correspondente do SQL Server 2019 CU5. As implantações do BDC anteriores ao CU5 existentes não serão afetadas por essa alteração, e os aplicativos nesses clusters continuarão sendo executados como usuário raiz. 

## <a name="technical-background"></a>Experiência técnica

Examine [este white paper técnico](https://aka.ms/sql-bdc-openshift-security) que captura detalhes do design de segurança para acomodar implantações que usam usuários não raiz, realçando quais Clusters de Big Data elevam temporariamente as permissões em certos casos e por que isso ocorre. O conteúdo do white paper foi desenvolvido em colaboração com especialistas em segurança do SQL Server e Red Hat, além de se concentrar em contextos de segurança e nas funcionalidades no OpenShift, mas os conceitos de segurança e o design do BDC são aplicáveis a todas as plataformas com suporte.

> [!NOTE]
> No momento do lançamento do CU5, a etapa de configuração dos aplicativos implantados com interfaces de [implantação de aplicativo](concept-application-deployment.md) ainda será executada como usuário *raiz*. Isso é necessário porque, durante a instalação, são instalados mais pacotes que o aplicativo usará. Outro código de usuário implantado como parte do aplicativo será executado como usuário de baixo privilégio. 

> [!NOTE]
> Recomendamos que o cluster seja executado com a configuração não raiz padrão. Caso você queira reverter para o comportamento anterior ao CU5 e tenha contêineres dentro do BDC que são executados como usuário `root`, você pode usar a nova opção de recurso `allowRunAsRoot` e desligar o comportamento padrão. Você só pode definir isso no momento da implantação. Para definir isso, especifique a configuração na seção `security` no arquivo de configuração de implantação `control.json`:

```json
 "security": {
  …
    "allowRunAsRoot": true,
  …
}
```

> [!IMPORTANT]
> Não há suporte para a alteração dessa configuração em ambientes OpenShift.

Como resultado dos serviços no BDC em execução como usuários não raiz, as credenciais usadas para se conectar a serviços por meio do ponto de extremidade do gateway não estão usando nome de usuário `root`. Se o aplicativo usado para se conectar ao ponto de extremidade do gateway estiver usando as credenciais erradas, você verá um erro de autenticação. O novo nome de usuário para o ponto de extremidade do gateway é baseado no valor passado pela variável de ambiente `AZDATA_USERNAME`. É o mesmo nome de usuário usado para os pontos de extremidade do controlador e do SQL Server. Isso afeta apenas as novas implantações; os Clusters de Big Data existentes implantados com qualquer uma das versões anteriores continuam usando `root`. Não há nenhum impacto nas credenciais quando o cluster é implantado para usar a autenticação do Active Directory. 

## <a name="use-the-latest-azure-data-studio"></a>Usar o Azure Data Studio mais recente

O Azure Data Studio manipula a alteração de credenciais de maneira transparente para a conexão realizada por meio do gateway para permitir uma experiência de navegação do HDFS no Pesquisador de Objetos ou o envio de trabalhos do Spark por meio de notebooks. Instale o [build para insiders do Azure Data Studio mais recente](../azure-data-studio/download-azure-data-studio.md#download-insiders-build-of-azure-data-studio). Esse build inclui as alterações necessárias para esse caso de uso.

Para outros cenários em que você deve fornecer credenciais para acessar o serviço por meio do gateway (por exemplo, fazer logon com [!INCLUDE [azure-data-cli-azdata](../includes/azure-data-cli-azdata.md)], acessar painéis da Web para Spark), verifique se as credenciais corretas são usadas. Se estiver direcionando um cluster existente implantado antes do CU5, você continuará usando o nome de usuário `root` para se conectar ao gateway, mesmo depois de atualizar o cluster para o CU5. Se você implantar um novo cluster usando o build do CU5, você fará logon fornecendo o nome de usuário correspondente à variável de ambiente `AZDATA_USERNAME`.

## <a name="configuration-file-switches"></a>Opções do arquivo de configuração

Do CU5 em diante, duas novas opções de recursos foram adicionadas para controlar a coleta de métricas de pod e nó. Caso você esteja usando soluções diferentes para monitorar sua infraestrutura de Kubernetes, é possível desativar a coleção de métricas internas para nós de pods e de host definindo `allowNodeMetricsCollection` e `allowPodMetricsCollection`* como `false` no arquivo de configuração de implantação `control.json`. 

Por exemplo 

```json
"security": {
  ...
  "allowPodMetricsCollection": true,
  "allowNodeMetricsCollection": true,
  ...
}
```

> [!NOTE]
> Para ambientes OpenShift, essas configurações são definidas como false por padrão nos perfis de implantação internos. A coleta de métricas de pod e de nó exigia funcionalidades privilegiadas e o contexto de segurança recomendado para OpenShift é baseado em limitações *restritas*.

Além de contêineres sem privilégios, começando com o CU5, para todas as novas implantações do BDC, os contêineres são executados como um usuário não raiz por padrão em todas as plataformas com suporte. Essas funcionalidades estão disponíveis para todas as novas implantações usando a marca de imagem correspondente do SQL Server 2019 CU5. As implantações do BDC anteriores ao CU5 existentes não serão afetadas, e os aplicativos nesses clusters continuarão sendo executados como usuário raiz.

## <a name="next-steps"></a>Próximas etapas
[Como implantar o [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no Kubernetes](deployment-guidance.md)

[Implantar [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)] no OpenShift](deploy-openshift.md)

[White paper de segurança](https://aka.ms/sql-bdc-openshift-security)
