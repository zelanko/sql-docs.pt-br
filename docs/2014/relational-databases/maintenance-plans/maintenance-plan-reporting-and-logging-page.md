---
title: Plano de manutenção (página Relatório e Log) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql12.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
manager: craigg
ms.openlocfilehash: 623507b4d9e52da376d4c83e4ee5c4d51b15dc39
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "63186266"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>Plano de manutenção (página Relatório e log)
  Use a caixa de diálogo **relatório e registro em log** para configurar os relatórios e os logs gerados quando os planos de manutenção são executados.  
  
## <a name="options"></a>Opções  
 **Gerar um relatório de arquivo de texto**  
 Especifique se deseja [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] gravar um relatório de arquivo de texto.  
  
 **Criar um novo arquivo**  
 Crie um arquivo de relatório novo para cada execução do plano de manutenção. Por padrão, os arquivos de relatório são gravados no computador de hospedagem da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém esse plano de manutenção, na pasta estabelecida como a pasta de log padrão, durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para especificar uma pasta diferente, digite o caminho completo da pasta na caixa de texto **Pasta** ou, clique no botão Procurar (**...**), e navegue até a pasta desejada.  
  
 **Acrescentar ao arquivo**  
 Anexe o relatório de cada plano de execução ao arquivo especificado na caixa de texto **Nome do arquivo** . Você também pode especificar um arquivo clicando no botão procurar e selecionando um arquivo na caixa de diálogo.  
  
 **Enviar relatório para um destinatário de email**  
 Transmita o resultado de um plano de manutenção por e-mail. Essa opção estará disponível apenas se o Database Mail estiver habilitado e configurado corretamente.  
  
 **Operador de agente**  
 Selecione na lista um operador do agente que será o recipiente do e-mail. Essa opção está disponível somente se o mail estiver habilitado corretamente  
  
 **Informações estendidas do log**  
 Inclua mais informações no log. A inclusão dessa opção aumentará o tamanho do histórico de plano de manutenção armazenado.  
  
 **Registrar no servidor remoto**  
 Registra o histórico do plano de manutenção em um servidor remoto.  
  
 **Conexão**  
 Especifica as informações de conexão a serem usadas ao fazer logon em um servidor remoto.  
  
 **Novo**  
 Exibe a caixa de diálogo **Propriedades da Conexão** . Usada para configurar informações de conexão novas para fazer o logon em um servidor remoto.  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](maintenance-plans.md)   
 [Database Mail](../database-mail/database-mail.md)  
  
  
