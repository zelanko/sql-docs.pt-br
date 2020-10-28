---
title: Solução de problemas de BDCs (Clusters de Big Data) com Jupyter notebooks e Azure Data Studio
titleSuffix: SQL Server Big Data Clusters
description: Solução de problemas de BDC com Jupyter notebooks e Azure Data Studio no cluster de Big Data do SQL Server 2019.
author: cloudmelon
ms.author: melqin
ms.reviewer: mikeray
ms.metadata: seo-lt-2019
ms.date: 09/22/2020
ms.topic: conceptual
ms.prod: sql
ms.technology: big-data-cluster
ms.openlocfilehash: 073776c042c0a0da136347c8e1658603b755208f
ms.sourcegitcommit: 29a2be59c56f8a4b630af47760ef38d2bf56a3eb
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 10/22/2020
ms.locfileid: "92378335"
---
# <a name="troubleshooting-big-data-clusters-bdc-with-notebooks"></a>Solução de problemas de BDC (Clusters de Big Data) com notebooks

Esta página é um índice de notebooks para Clusters de Big Data do SQL Server. Esses notebooks executáveis (.ipynb) foram criados para o SQL Server 2019 para auxiliar na solução de problemas de Clusters de Big Data.

Cada notebook foi criado para conferir suas próprias dependências. Um **Executar todas as células** vai ser concluído com êxito ou gerar uma exceção com uma dica de hiperlink para um outro notebook resolver a dependência ausente. Siga o hiperlink de dica para o notebook subsequente, pressione **Executar todas as células** e, tendo êxito, volte para o notebook original e pressione **Executar todas as células** .

Depois que todas as dependências forem instaladas mas **Executar todas as células** falhar, cada notebook analisará os resultados e, sempre que possível, produzirá um hiperlink de dica para outro notebook a fim de ajudar a resolver o problema.


## <a name="troubleshooting-big-data-cluster-bdc"></a>Solução de problemas de BDC (cluster de Big Data)

Essa seção contém um conjunto de notebooks para obtenção de logs de um BDC (cluster de Big Data) do SQL Server.

|Name |Descrição |
|---|---|---|---|
|TSG100 – Solução de problemas do Cluster de Big Data|Visão geral de todos os notebooks disponíveis sobre solução de problemas do BDC (cluster de Big Data) e de quando usá-los  |
|TSG101 – Solução de problemas do SQL Server|Visão geral de todos os notebooks disponíveis sobre solução de problemas do SQL Server e de quando usá-los  |
|TSG102 – Solução de problemas do HDFS|Visão geral de todos os notebooks disponíveis sobre solução de problemas do HDFS e de quando usá-los  |
|TSG103 – Solução de problemas do Spark|Visão geral de todos os notebooks disponíveis sobre solução de problemas do Spark e de quando usá-los  |
|TSG104 – Solução de problemas do controle|Visão geral de todos os notebooks disponíveis sobre solução de problemas de controlador e de quando usá-los  |
|TSG105 – Solução de problemas do gateway|Visão geral de todos os notebooks disponíveis sobre solução de problemas do Gateway do Knox e de quando usá-los  |
|TSG106 – Solução de problemas do aplicativo|Visão geral de todos os notebooks disponíveis sobre solução de problemas de App-Deploy e de quando usá-los  |



## <a name="diagnose-issues-from-big-data-clusters-bdc"></a>Diagnosticar problemas de BDCs (Clusters de Big Data)

Um conjunto de notebooks para diagnosticar situações e estados com um cluster de Big Data.

|Name |Descrição |
|---|---|---|---|
|TSG002 – CrashLoopBackoff|Esse TSG se conectará a cada contêiner cuja última tentativa de entrar em um estado 'Em execução' falhou e obterá os logs de contêiner atuais e anteriores. Isso é útil para depurar problemas de CrashLoopBackOff relatados em kubectl get pods.|
|TSG025 – Navegador do FSM – consultar o estado do FSM do controlador|Use esse notebook para se conectar ao banco de dados do controlador e procurar o estado do FSM (Máquina de Estado Finito). Use este notebook para listar os computadores de estado ativo e identificar os fluxos de trabalho travados.|
|TSG026 – Conectar-se ao nó do pool de dados (para executar o T-SQL)|Use esse notebook para conectar-se ao nó do pool de dados (para executar o T-SQL)|
|TSG027 – Observar a implantação de cluster|Use esse notebook para observar a implantação do cluster. Ele fornece diretrizes para solução de problemas de criação do cluster de Big Data do SQL Server, e os comandos a seguir geralmente são úteis para identificar as causas subjacentes. |
|TSG029 – Localizar despejos no cluster|Use esse notebook para procurar despejos principais e minidespejos de processos como SQL Server ou o controlador em um cluster de Big Data.|
|TSG032 – Uso da CPU e de memória para todos os contêineres|Use esse notebook para verificar o uso da CPU e de memória para todos os contêineres.|
|TSG037 – Determinar o pod do pool mestre que hospeda a réplica primária|Use esse notebook para determinar o pod do pool mestre que hospeda a réplica primária para o cluster de Big Data quando a alta disponibilidade do pool mestre estiver habilitada.|
|TSG044 – Executar sqlcmd no contêiner do pool mestre|Use esse notebook para conectar-se a um nó do pool mestre diretamente por meio do T-SQL.|
|TSG055 – Tempo da cURL para o Sparkhead|Use esse notebook para uma etapa de diagnóstico visando entender qual é o tempo de resposta da cURL do pod do controlador para o pod do Sparkhead.|
|TSG060 – Espaço em disco para Volume Persistente para todos os PVCs do BDC|Use esse notebook para se conectar a cada contêiner e obtenha o espaço em disco usado/disponível para cada PV (Volume Persistente) mapeado para cada PVC (Declaração de Volume Persistente) de um BDC (Cluster de Big Data).|
|TSG078 – O cluster está íntegro|Use esse notebook para verificar se o seu BDC (cluster de Big Data) está íntegro.|
|TSG079 – Gerar despejo de núcleo do controlador|Use esse notebook para gerar um despejo de núcleo do controlador.|
|TSG086 – Executar top em todos os contêineres|Use esse notebook para executar top em todos os contêineres.|
|TSG087 – Usar a CLI do Hadoop FS no pod do namenode|Use esse notebook para usar a CLI do Hadoop FS no pod do namenode.|
|TSG108 – Ver o mapa de configurações de atualização do controlador|Use esse notebook para solucionar a falha ao executar uma atualização de cluster de Big Data usando **azdata bdc upgrade** .|
|TSG112 – Verificações pré-implantação do Active Directory|Use esse notebook para validar se uma configuração de BDC (cluster de Big Data) é válida para uma implantação do AD (Active Directory).|
|TSG115 – Conversor de log de segurança de SQL Server em Linux|Use esse notebook para analisar os logs gerados pelos agentes secuirty.ldap e security.kerberos para SQL Server em Linux. Para habilitar esses agentes, coloque as linhas abaixo em /var/opt/mssql/logger.ini no computador que executa o SQL Server em Linux. Observação: esse arquivo diferencia maiúsculas de minúsculas.|
|TSG116 – Conversor de log de suporte de segurança do BDC do SQL|Use esse notebook para analisar os logs gerados pelo serviço de suporte de segurança no BDC do SQL. Para obter os logs, copiaremos os logs de depuração do cluster e os extrairemos. Siga as etapas abaixo – execute "azdata bdc debug copy-logs -n <namespace> *". Isso criará vários arquivos .tar.gz – Extraia o conteúdo de debuglogs-* <namespace>-<date>-<time>.tar.gz – Localize o log de suporte de segurança armazenado em ./<namespace>/control-<…>/security-support/supervisol/log/secsupp-stderr---<…>.log.|
|TSG119 – Verificações pós-implantação do Active Directory|Esse notebook foi projetado para validar a configuração do BDC após uma implantação do AD. Ele verificará a existência de entradas DNS para todos os pontos de extremidade com um atributo dnsName e essas entradas DNS devem ser registros de host, não aliases (ou seja, registros A, não registros CNAME). Ele verificará também a existência de contas do AD conhecidas e se elas estão habilitadas, bem como a existência dos SPNs esperados|






## <a name="repair-issues-from-big-data-clusters-bdc"></a>Reparo de problemas de BDCs (Clusters de Big Data)

Um conjunto de notebooks destinados a reparar situações e estados conhecidos de um cluster de Big Data do SQL Server.

|Name |Descrição |
|---|---|---|---|
|TSG005 – Loop de encaminhamento detectado|Use esse notebook para lidar com situações em que um loop de encaminhamento foi detectado, já que o utilitário dnsmasq pode colocar um loopback local em resolv.conf, o que pode fazer com que os pods do controlador entrem em um CrashLoopBackOff durante a implantação inicial do cluster: https://askubuntu.com/questions/627899/nameserver-127-0-1-1-in-resolv-conf-wont-go-away|
|TSG011 – Reiniciar o servidor sparkhistory|Use esse notebook para reiniciar o servidor sparkhistory, pois o processo Java do sparkhistory pode travar durante a inicialização. A reinicialização do servidor sparkhistory (supervisorctl restart sparkhistory) pode resolver esse problema.|
|TSG018 – Encerrar o processo sqlservr no pool mestre| Use esse notebook quando o desligamento do T-SQL não reciclar com êxito o processo ./sqlservr. Use esse notebook para encerrar o processo principal sqlservr que será reiniciado automaticamente pelo processo de front-end ./sqlservr.|
|TSG024 – O Namenode está no modo de segurança| Use esse notebook quando o HDFS entrar por conta própria em modo de segurança. Por exemplo, se muitos pods forem reciclados muito rapidamente no pool de armazenamento, o modo de segurança poderá ser habilitado automaticamente.|
|TSG028 – Reiniciar o gerenciador de nós em todos os nós do pool de armazenamento| Use esse notebook quando for necessário reiniciar o gerenciador de nós em todos os nós do pool de armazenamento.|
|TSG038 – Falhas na criação do BDC devido à chave ausente no documento| Use esse notebook quando ocorrerem falhas na criação do BDC devido a uma chave ausente no documento.|
|TSG039 – Nome de objeto 'role_permissions' inválido| Use esse notebook quando você tiver um problema de objeto inválido devido à permissão de função em Knox gateway.log|
|TSG040 – Falha ao obter nomes de arquivo do controlador com o erro| Use esse notebook quando você enfrentar um erro 504 – Tempo limite do gateway ao obter nomes de arquivo do controlador.|
|TSG041 – Não é possível criar um contexto de E/S assíncrona (aumentar sysctl fs.aio-max-nr)| Use esse notebook quando você não conseguir criar um contexto de E/S assíncrona (aumentar sysctl fs.aio-max-nr).|
|TSG045 – O número máximo de discos de dados que podem ser anexados a uma VM deste tamanho (AKS)| Use esse notebook quando o número máximo de discos de dados que podem ser anexados a uma VM deste tamanho (AKS) for alcançado.|
|TSG047 – ConfigException – esperado apenas um objeto com nome| Use esse notebook quando encontrar uma ConfigException, que estará esperando apenas um objeto com nome.|
|TSG048 – Implantação travada em "Aguardando o pod do controlador ficar ativo"| Use esse notebook quando a implantação tiver travado em "Aguardando o pod do controlador ficar ativo".|
|TSG050 – A criação de cluster trava com "tempo limite expirado aguardando volumes a serem anexados ou montados para o pod"| Use esse notebook quando a criação de cluster travar com "tempo limite expirado aguardando que volumes sejam anexados ou montados para o pod".|
|TSG052 – Falha na tentativa de obter o DNS do master-svc e nova tentativa| Use esse notebook quando a criação de cluster travar com "tempo limite expirado aguardando que volumes sejam anexados ou montados para o pod".|
|TSG057 – Falha ao iniciar o serviço do controlador .System.TimeoutException| Use esse notebook quando você iniciar o serviço do controlador e obtiver System.TimeoutException.|
|TSG067 – Falha ao concluir a instalação da configuração de kube| Use esse notebook quando você enfrentar uma falha ao concluir a configuração de kube.|
|TSG074 – Excluir App-Deploys| Use esse notebook quando você tiver problemas para excluir aplicativos no cluster do BDC.|
|TSG075 – FailedCreatePodSandBox devido à falha de CNI de NetworkPlugin em configurar o pod| Use esse notebook quando você enfrentar uma exceção FailedCreatePodSandBox devido a uma falha de CNI de NetworkPlugin em configurar o pod.|
|TSG080 – Excluir as sessões do Spark usando o azdata| Use esse notebook ao encontrar um problema para excluir sessões do Spark.|
|TSG109 – Definir tempos limite de atualização| Use esse notebook quando enfrentar problemas para atualizar o BDC.|
|TSG110 – O Azdata retorna ApiError| Use esse notebook quando o Azdata retornar ApiError.|

## <a name="next-steps"></a>Próximas etapas

Para obter mais informações sobre clusters de Big Data, confira [O que são [!INCLUDE[big-data-clusters-2019](../includes/ssbigdataclusters-ss-nover.md)]](big-data-cluster-overview.md).

