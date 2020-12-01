---
description: Plano de manutenção (página Relatório e log)
title: Plano de manutenção (página Relatório e Log) | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: database-engine
ms.reviewer: ''
ms.technology: supportability
ms.topic: conceptual
f1_keywords:
- sql13.swb.maint.reportinglogging.f1
ms.assetid: 3a30b17a-3deb-446f-900a-62f88934a90f
author: MikeRayMSFT
ms.author: mikeray
ms.openlocfilehash: 05db1c0f8c2eacd2a30e1e1e50b08e090ca6e9c4
ms.sourcegitcommit: c5078791a07330a87a92abb19b791e950672e198
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/26/2020
ms.locfileid: "88420860"
---
# <a name="maintenance-plan-reporting-and-logging-page"></a>Plano de manutenção (página Relatório e log)
 [!INCLUDE [SQL Server](../../includes/applies-to-version/sqlserver.md)]
  Use a caixa de diálogo **Relatório e Log** , para configurar os relatórios e logs gerados quando os planos de manutenção são executados.  
  
## <a name="options"></a>Opções  
 **Gerar um relatório de arquivo de texto**  
 Especifique se deseja que o [!INCLUDE[msCoName](../../includes/msconame-md.md)] [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] grave um relatório de arquivo de texto.  
  
 **Criar um arquivo**  
 Crie um arquivo de relatório novo para cada execução do plano de manutenção. Por padrão, os arquivos de relatório são gravados no computador de hospedagem da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que contém esse plano de manutenção, na pasta estabelecida como a pasta de log padrão, durante a instalação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para especificar uma pasta diferente, digite o caminho completo da pasta na caixa de texto **Pasta** ou, clique no botão Procurar (**...**), e navegue até a pasta desejada.  
  
 **Anexar ao arquivo**  
 Anexe o relatório de cada plano de execução ao arquivo especificado na caixa de texto **Nome do arquivo** . Você também pode especificar um arquivo clicando no botão procurar e selecionando um arquivo na caixa de diálogo.  
  
 **Enviar relatório a um recipiente de e-mail**  
 Transmita o resultado de um plano de manutenção por e-mail. Essa opção estará disponível apenas se o Database Mail estiver habilitado e configurado corretamente.  
  
 **Operador do agente**  
 Selecione na lista um operador do agente que será o recipiente do e-mail. Essa opção está disponível somente se o mail estiver habilitado corretamente  
  
 **Informações estendidas em log**  
 Inclua mais informações no log. A inclusão dessa opção aumentará o tamanho do histórico de plano de manutenção armazenado.  
  
 **Registrar no servidor remoto**  
 Registra o histórico do plano de manutenção em um servidor remoto.  
  
 **Conexão**  
 Especifica as informações de conexão a serem usadas ao fazer logon em um servidor remoto.  
  
 **Novo**  
 Exibe a caixa de diálogo **Propriedades da Conexão** . Usada para configurar informações de conexão novas para fazer o logon em um servidor remoto.  
  
## <a name="see-also"></a>Consulte Também  
 [Planos de manutenção](../../relational-databases/maintenance-plans/maintenance-plans.md)   
 [Database Mail](../../relational-databases/database-mail/database-mail.md)  
  
  
