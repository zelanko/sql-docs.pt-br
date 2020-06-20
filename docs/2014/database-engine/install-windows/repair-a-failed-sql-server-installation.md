---
title: Reparar uma instalação do SQL Server 2014 | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: install
ms.topic: conceptual
ms.assetid: 90c11b28-892b-44d6-978e-0eee48c75b7d
author: MashaMSFT
ms.author: mathoma
ms.openlocfilehash: 508167dcb0f263e319a2cf2f90c2eda3fbe2a714
ms.sourcegitcommit: 9ee72c507ab447ac69014a7eea4e43523a0a3ec4
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/17/2020
ms.locfileid: "84932107"
---
# <a name="drop-a-sql-server-2014-installation"></a>Descartar uma instalação do SQL Server 2014
  A operação de reparo pode ser usada nos seguintes cenários:  
  
-   Reparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] corrompida após instalação bem-sucedida.  
  
-   Reparar uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] se a operação de atualização for cancelada ou falhar depois que o nome da instância for mapeado para a instância recém-atualizada.  
  
    -   Se você encontrar a mensagem seguinte no log de resumo, poderá reparar a instância de atualização com falha:  
  
         Falha na atualização do "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para continuar, investigue o motivo da falha, corrija o problema e repare a instalação."  
  
    -   Se você encontrar a mensagem a seguir no log de resumo, será necessário desinstalar e reinstalar o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. Você não pode reparar a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
         Falha na atualização do "[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para continuar, investigue o motivo para a falha e corrija o problema".  
  
 Quando você repara uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]:  
  
-   Todos os arquivos ausentes ou corrompidos são substituídos.  
  
-   Todas as chaves do Registro ausentes ou corrompidas são substituídas.  
  
-   Todos os valores de configuração ausentes ou inválidos são definidos como valores padrão.  
  
 Antes de você continuar, para clusters de failover do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , examine as seguintes informações importantes:  
  
-   O reparo dever ser executado em nós de cluster individuais.  
  
-   Para reparar um nó de cluster de failover após uma operação Preparar com falha, use **Remover nó** e execute a etapa Preparar novamente. Para obter mais informações, consulte [Adicionar ou remover nós em um cluster de failover do SQL Server &#40;Instalação&#41;](../../sql-server/failover-clusters/install/add-or-remove-nodes-in-a-sql-server-failover-cluster-setup.md).  
  
### <a name="to-repair-a-failed-installation-of-ssnoversion-from-the-installation-center"></a>Para reparar uma instalação com falha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a partir da Central de Instalação  
  
1.  Inicie o programa de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (setup.exe) na mídia de instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
2.  Depois da verificação dos pré-requisitos e do sistema, o programa de Instalação exibirá a página Central de Instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
3.  Clique em **Manutenção** na área de navegação à esquerda e clique em **Reparar** para iniciar a operação de reparo.  
  
    > [!TIP]  
    >  Se a Central de Instalação foi iniciada usando o menu de início, você precisará fornecer o local da mídia de instalação neste momento.  
  
4.  A regra de suporte à Instalação e as rotinas de arquivos serão executadas para garantir que o sistema tenha os pré-requisitos instalados e que o computador seja aprovado nas regras de validação da Instalação. Clique em **OK** ou em **Instalar** para continuar.  
  
5.  Na página Selecionar Instância, selecione a instância a ser reparada e clique em **Avançar** para continuar.  
  
6.  As regras de reparo são executadas para validar a operação. Para continuar, clique em **Avançar**.  
  
7.  A página Pronto para Reparar indica que a operação está pronta para continuar. Para continuar, clique em **Reparar**.  
  
8.  A página de Progresso do Reparo mostra o status da operação de reparo. A página Concluído indica que a operação foi concluída.  
  
### <a name="to-repair-a-failed-installation-of-ssnoversion-using-command-prompt"></a>Para reparar uma instalação com falha do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usando um prompt de comando  
  
1.  Execute o seguinte comando em um prompt de comando:  
  
    ```  
    Setup.exe /q /ACTION=Repair /INSTANCENAME=instancename  
    ```  
  
## <a name="see-also"></a>Consulte Também  
 [Exibir e ler arquivos de log da Instalação do SQL Server](view-and-read-sql-server-setup-log-files.md)   
 [Tópicos de instruções sobre a instalação](../../sql-server/install/installation-how-to-topics.md)  
  
  
