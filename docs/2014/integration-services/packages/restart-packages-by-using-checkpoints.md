---
title: Reiniciar pacotes por meio de pontos de verificação | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
helpviewer_keywords:
- checkpoints [Integration Services]
- restarting packages
- starting packages
ms.assetid: 48f2fbb7-8964-484a-8311-5126cf594bfb
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 1f41ed858bedd18ec68794d5e7d1c13100af5254
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/25/2020
ms.locfileid: "62767028"
---
# <a name="restart-packages-by-using-checkpoints"></a>Reiniciar pacotes por meio de pontos de verificação
  [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] pode reinicializar pacotes que falharam a partir do ponto de falha, em vez de executar novamente todo o pacote. Se um pacote estiver configurado para usar pontos de verificação, serão gravadas informações sobre a execução do pacote em um arquivo de ponto de verificação. Quando o pacote com falha é executado novamente, o arquivo do ponto de verificação é usado para reiniciar o pacote a partir do ponto de falha. Se o pacote for executado com êxito, o arquivo de ponto de verificação é excluído e recriado na próxima vez que o pacote for executado.  
  
 Usar pontos de verificação em um pacote fornece os seguintes benefícios:  
  
-   Evite repetir o download e o upload de arquivos grandes. Por exemplo, um pacote que baixa diversos arquivos grandes usando uma tarefa FTP para cada download pode ser reiniciado após o download de um único arquivo falhar e baixar apenas aquele arquivo.  
  
-   Evite repetir o carregamento de grandes quantidades de dados. Por exemplo, um pacote que realiza inserções em massa em tabelas de dimensão em um data warehouse usando uma tarefa Inserção em Massa diferente para cada dimensão pode ser reiniciado se a inserção falhar em uma tabela de dimensão e apenas essa dimensão será recarregada.  
  
-   Evite repetir a agregação de valores. Por exemplo, um pacote que computa muitas agregações, como médias e somas, usando uma tarefa de Fluxo de Dados separada para realizar cada agregação, pode ser reiniciado após computar uma falha de agregação e somente essa agregação será computada novamente.  
  
 Se um pacote for configurado para usar pontos de verificação, o [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)] capturará o ponto de reinicialização no arquivo de ponto de verificação. O tipo de contêiner que falha e a implementação de recursos como transações afetam o ponto de reinicialização registrado no arquivo de ponto de verificação. Os valores atuais das variáveis também são capturados no arquivo de ponto de verificação. No entanto, os valores de variáveis que têm o tipo de dados `Object` não são salvos em arquivos de ponto de verificação.  
  
## <a name="defining-restart-points"></a>Definindo os pontos de reinicialização  
 O contêiner host da tarefa que encapsula uma única tarefa é a menor unidade atômica de trabalho que pode ser reiniciada. O contêiner Loop Foreach e um contêiner transacionado também são tratados como unidades atômicas de trabalho.  
  
 Se um pacote for interrompido enquanto um contêiner transacionado estiver executando, a transação será encerrada e qualquer trabalho realizado pelo contêiner será revertido. Quando o pacote for reinicializado, o contêiner que falhou será executado novamente. A conclusão de qualquer contêiner filho de contêiner transacionado não é registrada no arquivo de ponto de verificação. Portanto, quando o pacote for reinicializado, o contêiner transacionado e seus contêineres filho serão executados novamente.  
  
> [!NOTE]  
>  O uso de pontos de verificação e transações no mesmo pacote pode gerar resultados inesperados. Por exemplo, quando um pacote falha e é reiniciado em um ponto de verificação, o pacote pode repetir uma transação que já tenha sido confirmada com êxito.  
  
 Os dados do ponto de verificação não são salvos para os contêineres Loop For e Loop Foreach. Quando um pacote é reinicializado, os contêineres Loop For e Loop Foreach e seus contêineres filho são executados novamente. Se um contêiner filho no loop executar com êxito, ele não será registrado no arquivo de ponto de verificação, ao invés disso ele será executado novamente. Para obter mais informações e uma solução alternativa, consulte [Pontos de verificação do SSIS não são honrados para itens de contêiner Loop For ou Loop Foreach](https://go.microsoft.com/fwlink/?LinkId=241633).  
  
 Se o pacote for reiniciado as configurações do pacote não serão recarregadas, ao invés disso o pacote usará as informações de configuração gravadas no arquivo de ponto de verificação. Isto assegura que o pacote usará as mesmas configurações existentes no momento que falhou quando for executado novamente.  
  
 Um pacote só pode ser reinicializado no nível de fluxo de controle. Não é possível reinicializar um pacote no meio de um fluxo de dados. Para evitar executar novamente todo o fluxo de dados, o pacote deve ser projetado para incluir diversos fluxos de dados, cada um usando uma tarefa de Fluxo de Dados diferente. Deste modo o pacote pode ser reinicializado, executando apenas uma tarefa de Fluxo de Dados novamente.  
  
## <a name="configuring-a-package-to-restart"></a>Configurando um pacote para reiniciar  
 O arquivo de ponto de verificação inclui os resultados da execução de todos os contêineres concluídos, os valores atuais do sistema e variáveis definidas pelo usuário e informações de configuração do pacote. O arquivo também inclui o identificador exclusivo do pacote. Para reiniciar um pacote com êxito, o identificador do pacote no arquivo de ponto de verificação e o pacote devem corresponder; caso contrário a reinicialização falhará. Isto impede um pacote de usar um arquivo de ponto de verificação escrito por uma versão de pacote diferente. Se o pacote executar com êxito, após sua reinicialização o arquivo do ponto de verificação é excluído.  
  
 A seguinte tabela lista as propriedades de pacote definidas para implementar pontos de verificação.  
  
|Propriedade|DESCRIÇÃO|  
|--------------|-----------------|  
|CheckpointFileName|Especifica o nome do arquivo de ponto de verificação.|  
|CheckpointUsage|Especifica se pontos de verificação são usados.|  
|SaveCheckpoints|Indica se o pacote salva os pontos de verificação. Esta propriedade deve ser definida como Verdadeiro para reinicializar um pacote a partir de um ponto de falha.|  
  
 Além disso, você deve definir a Propriedade FailPackageOnFailure `true` como para todos os contêineres no pacote que você deseja identificar como pontos de reinicialização.  
  
 É possível usar a propriedade ForceExecutionResult para testar o uso de pontos de verificação em um pacote. Ao definir ForceExecutionResult de uma tarefa ou contêiner como Falha, você pode imitar uma falha em tempo real. Ao executar novamente o pacote, a tarefa e os contêineres que falharam serão executados de novo.  
  
### <a name="checkpoint-usage"></a>Uso do ponto de verificação  
 A propriedade CheckpointUsage pode ser definida com os seguintes valores:  
  
|Valor|DESCRIÇÃO|  
|-----------|-----------------|  
|`Never`|Especifica que o arquivo de ponto de verificação não é usado e o pacote executa a partir do início do fluxo de trabalho do pacote.|  
|`Always`|Especifica que o arquivo de ponto de verificação sempre é usado e que o pacote reinicia a partir do ponto da falha de execução anterior. Se o arquivo de ponto de verificação não for localizado, o pacote falhará.|  
|`IfExists`|Especifica que o arquivo de ponto de verificação é usado, se existir. Se o arquivo de ponto de verificação existir, o pacote reiniciará a partir do ponto da falha de execução anterior; caso contrário, será executado desde o início do fluxo de trabalho do pacote.|  
  
> [!NOTE]  
>  A opção **/CheckPointing on on** de dtexec é equivalente a definir a `SaveCheckpoints` Propriedade do pacote como `True`e a `CheckpointUsage` Propriedade como Always. Para saber mais, veja [dtexec Utility](dtexec-utility.md).  
  
## <a name="securing-checkpoint-files"></a>Protegendo arquivos de ponto de verificação  
 A proteção em nível de pacote não inclui proteção a arquivos de ponto de verificação; você deve proteger esses arquivos separadamente. Dados de ponto de verificação podem ser armazenados somente no sistema arquivos e você deve usar uma ACL (lista de controle de acesso) do sistema operacional para proteger o local ou a pasta onde armazena o arquivo. É importante proteger os arquivos de ponto de verificação, pois eles contém informações sobre o estado do pacote, incluindo os valores atuais de variáveis. Por exemplo, uma variável pode conter um conjunto de registros com muitas linhas de dados particulares como números de telefone. Para obter mais informações, consulte [Acesso aos arquivos usados por pacotes](../access-to-files-used-by-packages.md).  
  
### <a name="to-configure-the-checkpoint-properties"></a>Para configurar as propriedades de ponto de verificação  
  
-   [Configurar pontos de verificação para reinicializar um pacote com falha](../configure-checkpoints-for-restarting-a-failed-package.md)  
  
## <a name="external-resources"></a>Recursos externos  
  
-   Artigo técnico, [Reinicialização automática de pacotes de SSIS depois de Failover ou Falha](https://go.microsoft.com/fwlink/?LinkId=200407), em social.technet.microsoft.com (a página pode estar em inglês)  
  
-   ARtigo de suporte, [Pontos de verificação do SSIS não são honrados para itens de contêiner Loop For ou Loop Foreach](https://go.microsoft.com/fwlink/?LinkId=241633), em support.microsoft.com.  
  
## <a name="see-also"></a>Consulte Também  
 [SQL Server Integration Services](../sql-server-integration-services.md)  
  
  
