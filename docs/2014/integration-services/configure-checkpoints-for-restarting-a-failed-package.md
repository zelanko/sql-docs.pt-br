---
title: Configurar pontos de verificação para reiniciar um pacote com falha | Microsoft Docs
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
ms.assetid: 9afffa5a-d803-4653-8afc-386453fc163f
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: e22e47af568ecf723b54a35fb6b83bd5ce74e333
ms.sourcegitcommit: 6fd8c1914de4c7ac24900fe388ecc7883c740077
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/26/2020
ms.locfileid: "66060766"
---
# <a name="configure-checkpoints-for-restarting-a-failed-package"></a>Configurar pontos de verificação para reinicializar um pacote com falha
  Você pode configurar os pacotes [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] para reiniciá-los a partir de um ponto de falha em vez de executar novamente todo o pacote, selecionando as propriedades que se aplicam aos pontos de verificação.  
  
### <a name="to-configure-a-package-to-restart"></a>Para configurar um pacote para reinicialização  
  
1.  No [!INCLUDE[ssBIDevStudioFull](../includes/ssbidevstudiofull-md.md)], abra o projeto do [!INCLUDE[ssISnoversion](../includes/ssisnoversion-md.md)] que contém o pacote que você deseja configurar.  
  
2.  Em **Gerenciador de soluções**, clique duas vezes no pacote para abri-lo.  
  
3.  Clique na guia **Fluxo de Controle** .  
  
4.  Clique com o botão direito do mouse em qualquer lugar da tela de fundo da superfície de design do fluxo de controle e clique em **Propriedades**.  
  
5.  Defina a Propriedade SaveCheckpoints como `True`.  
  
6.  Digite o nome do arquivo de ponto de verificação na propriedade CheckpointFileName.  
  
7.  Defina a propriedade CheckpointUsage como um dos dois valores:  
  
    -   Selecione `Always` para reiniciar o pacote partindo sempre de um ponto de verificação.  
  
        > [!IMPORTANT]  
        >  Um erro ocorrerá se o arquivo do ponto de verificação não estiver disponível.  
  
    -   Selecione `IfExists` para reiniciar o pacote apenas se o arquivo de ponto de verificação estiver disponível.  
  
8.  Configure as tarefas e os contêineres a partir dos quais o pacote pode ser reiniciado.  
  
    -   Clique com o botão direito do mouse em uma tarefa ou contêiner e clique em **Propriedades**.  
  
    -   Defina a Propriedade FailPackageOnFailure como `True` para cada tarefa e contêiner selecionados.  
  
## <a name="see-also"></a>Consulte Também  
 [Reiniciar pacotes por meio de pontos de verificação](packages/restart-packages-by-using-checkpoints.md)  
  
  
