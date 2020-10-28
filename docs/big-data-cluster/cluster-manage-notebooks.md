---
title: Gerenciar BDCs (Clusters de Big Data) com Jupyter notebooks e Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Gerenciamento de BDCs (Clusters de Big Data) com Jupyter notebooks e Azure Data Studio no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: e549a8005144e85a20cf613ff6695d11f7ff030f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378333"
---
# <a name="manage-big-data-clusters-bdc-the-cluster-with-notebooks"></a>Gerenciar BDCs (Clusters de Big Data) com notebooks

Esta página é um índice de notebooks para Clusters de Big Data do SQL Server. Esses notebooks executáveis (.ipynb) foram criados para o SQL Server 2019 para auxiliar no gerenciamento de Clusters de Big Data.

Cada notebook foi criado para conferir suas próprias dependências. Um **Executar todas as células** vai ser concluído com êxito ou gerar uma exceção com uma dica de hiperlink para um outro notebook resolver a dependência ausente. Siga o hiperlink de dica para o notebook subsequente, pressione **Executar todas as células** e, tendo êxito, volte para o notebook original e pressione **Executar todas as células** .

Depois que todas as dependências forem instaladas mas **Executar todas as células** falhar, cada notebook analisará os resultados e, sempre que possível, produzirá um hiperlink de dica para outro notebook a fim de ajudar a resolver o problema.


## <a name="installing-and-uninstalling-utilities-on-big-data-cluster-bdc"></a>Instalar e desinstalar utilitários no BDC (cluster de Big Data)

Essa seção contém um conjunto de notebooks útil para instalar e desinstalar pacotes e ferramentas de linha de comando necessários para gerenciar Clusters de Big Data do SQL Server.

|Name |Descrição |
|---|---|---|---|
|SOP010 – Atualizar um cluster de Big Data|Use esse notebook para atualizar um cluster de Big Data usando o azdata. |
|SOP012 – Instalar o unixodbc para Mac|Use esse notebook quando encontrar erros ao usar brew para instalar o ODBC para SQL Server.|
|SOP036 – Instalar a interface de linha de comando kubectl|Use esse notebook para instalar a interface de linha de comando do kubectl independentemente do seu sistema operacional.|
|SOP037 – Desinstalar a interface de linha de comando do kubectl|Use esse notebook para desinstalar a interface de linha de comando do kubectl independentemente do seu sistema operacional.|
|SOP038 – Instalar a interface de linha de comando do Azure|Use esse notebook para instalar a interface de linha de comando da CLI do Azure independentemente do seu sistema operacional.|
|SOP039 – Desinstalar a interface de linha de comando do Azure|Use esse notebook para desinstalar a interface de linha de comando da CLI do Azure independentemente do seu sistema operacional.|
|SOP040 – Atualizar pip na área restrita Python do ADS|Use esse notebook para atualizar o pip na área restrita do Python do ADS.|
|SOP054 – Instalar a interface de linha de comando do azdata|Use esse notebook para instalar a interface de linha de comando do azdata independentemente do seu sistema operacional.|
|SOP055 – Desinstalar a interface de linha de comando do azdata|Use esse notebook para desinstalar a interface de linha de comando do azdata independentemente do seu sistema operacional.|
|SOP059 – Instalar o módulo do Kubernetes do Python|Use esse notebook para instalar os módulos do Kubernetes com o Python.|
|SOP060 – Desinstalar o módulo do Kubernetes|Use esse notebook para desinstalar os módulos do Kubernetes com o Python.|
|SOP061 – Excluir um cluster de Big Data|Use esse notebook para excluir um cluster do BDC.|
|SOP062 – Instalar os módulos ipython-sql e pyodbc|Use esse notebook para instalar os módulos ipython-sql e pyodbc.|
|SOP063 – Instalar a CLI do azdata (usando o gerenciador de pacotes)|Use esse notebook para instalar a CLI do azdata (usando o gerenciador de pacotes).|
|SOP064 – Desinstalar a CLI do azdata (usando o gerenciador de pacotes)|Use esse notebook para desinstalar a CLI do azdata (usando o gerenciador de pacotes).|
|SOP069 – Instalar o ODBC for SQL Server|Use esse notebook para instalar o driver ODBC, já que alguns subcomandos no azdata exigem o driver ODBC do SQL Server.|


## <a name="managing-certificates-on-big-data-clusters-bdc"></a>Gerenciar certificados em BDCs (Clusters de Big Data)

Um conjunto de notebooks para executar um notebook para gerenciar certificados em Clusters de Big Data.

|Name |Descrição |
|---|---|---|---|
|CER001 – Gerar um Certificado de Autoridade de Certificação raiz|Gere um Certificado de Autoridade de Certificação raiz. Considere usar um Certificado de Autoridade de Certificação raiz para todos os clusters de não produção em cada ambiente, pois essa técnica reduz o número de certificados de AC raiz que precisam ser carregados para clientes que se conectam a esses clusters. |
|CER002 – Baixar um Certificado de Autoridade de Certificação raiz existente|Use esse notebook para baixar um Certificado de Autoridade de Certificação raiz gerado de um cluster.|
|CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente|CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente.|
|CER004 – Baixar e carregar um Certificado de Autoridade de Certificação raiz existente|Baixe e carregue um Certificado de Autoridade de Certificação raiz existente. |
|CER010 – Instalar a AC raiz gerada localmente|Esse notebook copiará localmente (de um cluster de Big Data) o Certificado de Autoridade de Certificação raiz gerado que foi instalado usando **CER001 – Gerar um Certificado de Autoridade de Certificação raiz** ou **CER003 – Carregar o Certificado de Autoridade de Certificação raiz existente** e instalará o Certificado de Autoridade de Certificação raiz no repositório de certificados local desse computador.|
|CER020 – Criar um certificado de proxy de gerenciamento|Esse notebook cria um certificado para o ponto de extremidade de proxy de gerenciamento.|
|CER021 – Criar certificado Knox|Esse notebook cria um certificado para o ponto de extremidade de gateway Knox.|
|CER022 – Criar certificado de proxy de aplicativo|Esse notebook cria um certificado para o ponto de extremidade de proxy de implantação de aplicativo.|
|CER023 – Criar certificado mestre|Esse notebook cria um certificado para o ponto de extremidade mestre.|
|CER030 – Assinar o certificado de proxy de gerenciamento com a AC gerada|Esse notebook assina o certificado criado usando **CER020 – Criar um certificado de proxy de gerenciamento** com o Certificado de Autoridade de Certificação raiz criado usando **CER001 – Gerar um Certificado de Autoridade de Certificação raiz** ou **CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente**|
|CER031 – Assinar um certificado Knox com uma AC gerada|Esse notebook assina o certificado criado usando **CER021 – Criar um certificado Knox** com o Certificado de Autoridade de Certificação raiz criado usando **CER001 – Gerar um Certificado de Autoridade de Certificação raiz** ou **CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente**|
|CER032 – Assinar o certificado de proxy de aplicativo com a AC gerada|Esse notebook assina o certificado criado usando **CER022 – Criar um certificado de proxy de aplicativo** com o Certificado de Autoridade de Certificação raiz criado usando **CER001 – Gerar um Certificado de Autoridade de Certificação raiz** ou **CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente** .|
|CER033 – Assinar um certificado mestre com uma AC gerada|Esse notebook assina o certificado criado usando **CER023 – Criar um certificado mestre** com o Certificado de Autoridade de Certificação raiz criado usando **CER001 – Gerar um Certificado de Autoridade de Certificação raiz** ou **CER003 – Carregar um Certificado de Autoridade de Certificação raiz existente** .|
|CER040 – Instalar um certificado de proxy de gerenciamento assinado|Esse notebook é instala o certificado assinado no cluster de Big Data usando **CER030 – Assinar o certificado de proxy de gerenciamento com a AC gerada** .|
|CER041 – Instalar um certificado Knox assinado|Esse notebook é instala o certificado assinado no cluster de Big Data usando **CER031 – Assinar um certificado Knox com uma AC gerada** .|
|CER042 – Instalar um certificado de proxy de aplicativo assinado|Esse notebook é instala o certificado assinado no cluster de Big Data usando **CER032 – Assinar o certificado de proxy de aplicativo com a AC gerada** .|
|CER043 – Instalar um certificado do Controlador assinado|O certificado assinado usando **CER034 – Assinar o certificado do Controlador com a AC raiz do cluster** é instalado por esse notebook no cluster de Big Data. Observe que, no final desse notebook, o pod do Controlador e todos os pods que usam o PolyBase (pods do pool de computação e do pool mestre) serão reiniciados para carregar os novos certificados.|
|CER050 – Aguardar que o BDC fique íntegro|Esse notebook aguardará até que o cluster de Big Data tenha retornado a um estado íntegro depois que o pod do Controlador e os pods que usam o PolyBase tiverem sido reiniciados para carregar os novos certificados.|
|CER100 – Configurar o cluster com certificados autoassinados|Esse notebook gerará uma nova AC raiz no cluster de Big Data e criará certificados para cada ponto de extremidade (esses pontos de extremidades são: Gerenciamento, Gateway, Proxy de Aplicativo e Controlador). Assine cada novo certificado com a nova AC raiz gerada, exceto o certificado do Controlador (que é assinado com a AC raiz do cluster existente) e instale cada certificado no cluster de Big Data. Baixe a nova AC raiz gerada no repositório de certificados das Autoridades de Certificação Raiz Confiáveis desse computador. Todos os certificados autoassinados gerados serão armazenados no pod do controlador na localização test_cert_store_root.|
|CER101 – Configurar o cluster com certificados autoassinados usando a AC raiz existente|Esse notebook usará uma AC raiz gerada existente no cluster de Big Data (carregada com **CER003** ), criará certificados para cada ponto de extremidade (Gerenciamento, Gateway, Aplicativo Proxy e Controlador), depois assinará cada novo certificado com a nova AC raiz gerada, exceto o certificado do Controlador (que é assinado com a AC raiz do cluster existente) e, por fim, instalará cada certificado no cluster de Big Data. Todos os certificados autoassinados gerados serão armazenados no pod do controlador (na localização test_cert_store_root). Após a conclusão desse notebook, todo o acesso https:// ao cluster de Big Data deste computador (e qualquer computador que instale a nova AC raiz) será exibido como sendo seguro. O capítulo do Executor do Notebook garantirá que o CronJobs criado (OPR003) para executar a implantação do aplicativo instale a AC raiz do cluster a fim de permitir que tokens JWT e o swagger.json sejam obtidos com segurança.|

## <a name="backup-and-restore-from-big-data-cluster-bdc"></a>Backup e restauração do BDC (cluster de Big Data)

Essa seção contém um conjunto de notebooks úteis para operações de backup e restauração para Clusters de Big Data do SQL Server.

| Name | Descrição |
|--|--|
| SOP008 – Fazer backup de arquivos do HDFS para o Azure Data Lake Storage Gen2 com distcp | Esse SOP (procedimento operacional padrão) fará backup dos dados do sistema de arquivos de origem do HDFS do cluster BDC do SQL Server 2019 para a conta do Azure Data Lake Storage Gen2 que você especificar. Verifique se a conta do Azure Data Lake Storage Gen2 está configurada com "namespace hierárquico" habilitado. |

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)], confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ver15.md)]?](big-data-cluster-overview.md).
