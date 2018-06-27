---
title: Como gerenciar uma instância CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/01/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.suite: sql
ms.technology: integration-services
ms.tgt_pltfrm: ''
ms.topic: conceptual
ms.assetid: 5d9e677f-b872-497d-9cde-472184a214ab
caps.latest.revision: 6
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: 925f81820422867d0580915647ca6245a2331b6e
ms.sourcegitcommit: cc46afa12e890edbc1733febeec87438d6051bf9
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/12/2018
ms.locfileid: "35409428"
---
# <a name="how-to-manage-a-cdc-instance"></a>How to Manage a CDC Instance
  Este procedimento descreve como usar o CDC Designer Console para gerenciar operações de instância CDC em tempo de execução.  
  
### <a name="to-manage-cdc-instance-operations"></a>Para gerenciar operações de instância CDC  
  
1.  No menu **Iniciar** , selecione o **CDC Designer Console**.  
  
2.  No painel esquerdo, expanda **Change Data Capture** e, em seguida, expanda o serviço que contém a instância que você quer exibir.  
  
3.  Selecione o nome de uma instância com a qual você quer trabalhar.  
  
4.  No painel **Ações** do lado direito do CDC Designer Console, clique na operação que você quer realizar.  
  
     Você também pode clicar com o botão direito no nome da instância no painel esquerdo e selecionar a operação que deseja realizar.  
  
     Você pode realizar as seguintes tarefas:  
  
    -   **Iniciar**: iniciar a captura de alterações.  
  
    -   **Parar**: parar a captura de alterações  
  
    -   **Redefinir**: clique em **Redefinir** para reiniciar a instância CDC a seu estado inicial (vazio). Esta opção está disponível quando a instância CDC é parada. Todas as alterações nas tabelas de alteração e o estado interno da instância CDC são excluídos. Quando a instância CDC é iniciada posteriormente, a captura de alterações inicia a partir desse ponto no tempo e só inclui transações iniciadas depois que a instância CDC iniciou.  
  
    -   **Excluir**: excluir a instância CDC.  
  
    -   **Oracle Logging Script**: clique em **Oracle Logging Script** para exibir a caixa de diálogo do script de registro em log do Oracle com o script de registro em log suplementar do Oracle. Para obter informações sobre o que você pode fazer nesta caixa de diálogo, consulte [Oracle Supplemental Logging Script](../../integration-services/change-data-capture/oracle-supplemental-logging-script.md).  
  
         **Observação**: quando você executa os scripts de log suplementares, a caixa de diálogo Oracle Credentials for Running Script abre e você fornece um nome de usuário e senha do Oracle válidos. Para obter informações sobre como fornecer as credenciais corretas do Oracle, consulte [Oracle Credentials for Running Script](../../integration-services/change-data-capture/oracle-credentials-for-running-script.md).  
  
    -   **CDC Instance Deployment**: gerar um script de implantação para a Instância CDC. Para obter informações sobre essa caixa de diálogo, consulte [CDC Instance Deployment Script](../../integration-services/change-data-capture/cdc-instance-deployment-script.md).  
  
     Para obter mais informações sobre estas tarefas, consulte [Manage a CDC Instance](../../integration-services/change-data-capture/manage-a-cdc-instance.md).  
  
 Você também pode selecionar **Propriedades** para editar as propriedades de configuração da instância CDC. Para obter mais informações sobre as propriedades da instância CDC, consulte [Edit Instance Properties](../../integration-services/change-data-capture/edit-instance-properties.md).  
  
  
