---
title: Propriedades de banco de dados (página Envio de Logs de Transações) | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: configuration
ms.topic: conceptual
f1_keywords:
- sql12.swb.databaseproperties.logshipping.f1
ms.assetid: 72c4e539-fe11-4d57-b977-65b418d5916f
author: stevestein
ms.author: sstein
manager: craigg
ms.openlocfilehash: 83ac357d01b616a0010b9c2132f77bbcf89b479b
ms.sourcegitcommit: f7fced330b64d6616aeb8766747295807c92dd41
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 04/23/2019
ms.locfileid: "62916997"
---
# <a name="database-properties-transaction-log-shipping-page"></a>Propriedades de banco de dados (página Envio do Logs de Transações)
  Use essa página para configurar e modificar as propriedades de envio de logs para um banco de dados.  
  
 Para obter uma explicação dos conceitos de envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Habilitar como banco de dados primário em uma configuração de envio de logs**  
 Habilita esse banco de dados como banco de dados primário para envio de logs. Selecione-o e, em seguida, configure as opções restantes na página. Se você desmarcar essa caixa de seleção, a configuração de envio de logs será descartada para esse banco de dados.  
  
 **Configurações de Backup**  
 Clique em **Configurações de Backup** para configurar o agendamento de backup, local, alerta e parâmetros de arquivamento.  
  
 **Agenda do Backup**  
 Mostra a agenda de backup selecionada presentemente para o banco de dados primário. Clique em **Configurações de Backup** para modificar essas configurações.  
  
 **Último Backup Criado**  
 Indica hora e data do último backup de log da transação do banco de dados primário.  
  
 **Instâncias e bancos de dados do servidor secundário**  
 Lista os servidores secundários presentemente configurados e os bancos de dados desse banco de dados primário. Destaque um banco de dados e depois clique em **...** para modificar os parâmetros associados àquele banco de dados secundário.  
  
 **Adicionar**  
 Clique em **Adicionar** para adicionar um banco de dados secundário à configuração de envio de logs para esse banco de dados primário.  
  
 **Remover**  
 Remove um banco de dados selecionado dessa configuração de envio de logs. Selecione primeiramente o banco de dados, depois clique em **Remover**.  
  
 **Use uma instância do servidor monitor**  
 Define uma instância de servidor monitor para essa configuração de envio de logs. Marque a caixa de seleção **Usar uma Instância de Servidor Monitor** , depois clique em **Configurações** para especificar a instância de servidor monitor.  
  
 **Instância de Servidor Monitor**  
 Indica a instância de servidor monitor atualmente configurada para essa configuração de envio de logs.  
  
 **Configurações**  
 Configura a instância de servidor monitor para uma configuração de envio de logs. Clique em **Configurações** para configurar essa instância de servidor monitor.  
  
 **Configuração do Script**  
 Gera um script para configuração do envio de logs com os parâmetros selecionados. Clique em **Configuração do script**, depois selecione um destino de saída para o script.  
  
> [!IMPORTANT]  
>  Antes de gerar scripts de configurações para um banco de dados secundário, é preciso chamar a caixa de diálogo **Configurações do Banco de Dados Secundário** . Chamar essa caixa de diálogo conecta você ao servidor secundário e recupera as configurações atuais do banco de dados secundário que são necessárias para gerar o script.  
  
## <a name="see-also"></a>Consulte também  
 [Procedimentos armazenados de envio de logs &#40;Transact-SQL&#41;](/sql/relational-databases/system-stored-procedures/log-shipping-stored-procedures-transact-sql)   
 [Tabelas de envio de logs &#40;Transact-SQL&#41;](/sql/relational-databases/system-tables/log-shipping-tables-transact-sql)  
  
  
