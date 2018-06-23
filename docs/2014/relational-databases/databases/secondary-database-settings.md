---
title: Configurações do Banco de Dados Secundário | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology:
- database-engine
ms.tgt_pltfrm: ''
ms.topic: article
f1_keywords:
- sql12.swb.databaseproperties.logshipping.settings.dest.f1
ms.assetid: f992ffc9-ee42-43fe-acec-512032f0ded1
caps.latest.revision: 31
author: craigg-msft
ms.author: craigg
manager: jhubbard
ms.openlocfilehash: d1227ddc27604e8cb8298e34d63b741cd57d0ebf
ms.sourcegitcommit: 5dd5cad0c1bbd308471d6c885f516948ad67dfcf
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 06/19/2018
ms.locfileid: "36009358"
---
# <a name="secondary-database-settings"></a>Configurações do Banco de Dados Secundário.
  Use essa caixa de diálogo para configurar e modificar as propriedades de um banco de dados secundário na configuração de envio de logs.  
  
 Para obter uma explicação dos conceitos de envio de log, veja [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md).  
  
## <a name="options"></a>Opções  
 **Instância de servidor secundário**  
 Exibe o nome da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] atualmente configurada para ser um servidor secundário em uma configuração do envio de logs.  
  
 **Banco de dados secundário**  
 Exibe o nome do banco de dados secundário para a configuração de envio de logs. Ao adicionar um novo banco de dados secundário a uma configuração de envio de logs, é possível escolher um banco de dados da lista ou digitar o nome de um novo do banco de dados na caixa. Se você digitar o nome de um novo banco de dados, deve-se selecionar a opção na guia **Inicialização** que restaura um backup de banco de dados completo do banco de dados primário para o banco de dados secundário. O banco de dados novo é criado como parte da operação de restauração.  
  
 **Connect**  
 Conecte-se a uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] a ser usada como servidor secundário em uma configuração do envio de logs. A conta usada para conexão precisa ser membro da função de servidor fixa sysadmin na instância de servidor secundário.  
  
 **Guia Inicialização**  
 As opções são as seguintes:  
  
 **Sim, gere um backup completo do banco de dados primário e restaure para o banco de dados secundário**  
 Use [!INCLUDE[ssManStudioFull](../../includes/ssmanstudiofull-md.md)] para configurar seu banco de dados secundário, fazendo o backup do banco de dados primário e restaurando-o no servidor secundário. Se você digitou um novo nome de banco de dados na caixa **Banco de dados secundário** , o banco de dados será criado com parte da operação de restauração.  
  
 **Opções de restauração**  
 Clique se desejar restaurar os dados e arquivos de log para o banco de dados secundário em locais não padrão no servidor secundário.  
  
 Esse botão abre a caixa de diálogo **Opções de Restauração** . Ali é possível especificar caminhos a pastas não padrão nos quais se deseja localizar o banco de dados secundário e seu log. Ao especificar qualquer pasta, deve-se especificar ambos.  
  
 Os caminhos devem se referir a unidades locais para o servidor secundário. Além disso, os caminhos devem começar com uma letra de unidade local e dois pontos (por exemplo, `C:`). Letras de unidades ou caminhos de rede mapeados não são válidos.  
  
 Se você clicar no botão **Opções de Restauração** e resolver que deseja usar as pastas padrão, recomendamos que cancele a caixa de diálogo **Opções de Restauração** . Se você já especificou locais não padrão e agora deseja usar locais padrão, clique novamente em **Opções de Restauração** desmarque as caixas de texto e clique em OK.  
  
 **Sim, restaure um backup existente do banco de dados primário para o banco de dados secundário**  
 Escolha [!INCLUDE[ssManStudio](../../includes/ssmanstudio-md.md)] para usar um backup existente de seu banco de dados primário para inicializar o banco de dados secundário. Digite o local daquele backup na caixa **Arquivo de backup** . Se você digitou um novo nome de banco de dados na caixa Banco de dados secundário, o banco de dados será criado como parte da operação de restauração.  
  
 **Arquivo de backup**  
 Digite o caminho e nome de arquivo do backup completo do banco de dados que deseja usar para inicializar o banco de dados secundário. Se escolher **Sim, restaurar um backup existente do banco de dados primário para o banco de dados secundário**.  
  
 **Opções de restauração**  
 Veja a descrição desse botão anteriormente neste tópico.  
  
 **Não, o banco de dados secundário é inicializado**  
 Especifique se o banco de dados secundário já foi inicializado e se está pronto para aceitar backups de log de transações do banco de dados primário. Essa opção não está disponível se você digitou um nome de banco de dados novo na caixa **Banco de dados secundário** .  
  
 **Guia Copiar Arquivos**  
 As opções são as seguintes:  
  
 **Pasta de destino dos arquivos copiados**  
 Digite o caminho para o qual deveriam ser copiados backups de log de transações para restauração para o banco de dados secundário. Normalmente, esse é um caminho local para uma pasta localizada no servidor secundário. Mas se a pasta estiver em outro servidor, você deve especificar um caminho UNC para a pasta. A conta de servidor [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] da instância do servidor secundário deve ter permissões de leitura nessa pasta. Você deve conceder também permissões de leitura e gravação para esse compartilhamento de rede para as contas proxy nas quais os trabalhos de cópia e restauração serão executados nas instâncias do servidor secundário. Por padrão, essa é a conta do serviço SQLServerAgent da instância do servidor secundário, mas um sysadmin pode escolher outras contas proxy para o trabalho.  
  
 **Excluir arquivos copiados após**  
 Escolha o período de tempo que deseja que os arquivos de backup de log de transações permaneçam na pasta de destino antes de serem excluídos.  
  
 **Nome do trabalho**  
 Exibe o nome do trabalho do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Agent usado para copiar arquivos de backup de log de transações do servidor primário para o servidor secundário. Ao criar esse trabalho pela primeira vez, é possível alterar o nome digitando-o na caixa.  
  
 **Agenda**  
 Exibe a agenda atual para o trabalho de cópia do SQL Server Agent para copiar backups do log de transações do servidor primário para o servidor secundário. É possível alterar essa agenda clicando-se em **Agenda....**  
  
 **Agenda....**  
 Modifique os parâmetros do trabalho do SQL Server Agent que copia backups de log de transações do servidor primário para o servidor secundário.  
  
 **Desabilitar este trabalho**  
 Suspenda o trabalho de cópia do SQL Server Agent.  
  
 **Guia Restaurar Log de Transações**  
 As opções são as seguintes:  
  
 **Desconectar usuários no banco de dados ao restaurar backups**  
 Desconecte usuários automaticamente do banco de dados secundário enquanto estão sendo restaurados os backups de log de transações.  
  
 **Nenhum modo de recuperação**  
 Deixe o banco de dados secundário em modo NORECOVERY.  
  
 **Modo de espera**  
 Deixe o banco de dados secundário em modo STANDBY. Esse modo permitirá a execução de operações somente leitura no banco de dados.  
  
> [!IMPORTANT]  
>  Se você alterar o modo de recuperação de um banco de dados secundário existente, por exemplo, de **Nenhum modo de recuperação** para **Modo de espera**, a alteração terá efeito somente depois do próximo backup de log ser restaurado no banco de dados.  
  
 **Atrasar restauração de backups pelo menos**  
 Escolha o atraso antes que os backups de log de transações sejam restaurados para o banco de dados secundário, se houver.  
  
 **Alertar se nenhuma restauração ocorrer em**  
 Escolha o período de tempo que você deseja que o envio de logs espere antes de acionar um alerta de que nenhuma restauração de backup de log de transações ocorreu.  
  
 **Nome do trabalho**  
 Exibe o nome do trabalho do SQL Server Agent usado para restaurar os backups do log de transações para o banco de dados secundário. Ao criar esse trabalho pela primeira vez, é possível alterar o nome digitando-o na caixa.  
  
 **Agenda**  
 Exibe a agenda atual para o trabalho do SQL Server Agent usado para restaurar os backups do log de transações para o banco de dados secundário. É possível alterar essa opção clicando-se em **Agenda....**  
  
 **Agenda....**  
 Modifique os parâmetros relacionados à restauração do trabalho do SQL Server Agent.  
  
 **Desabilitar este trabalho**  
 Suspenda operações de restauração para o banco de dados secundário.  
  
## <a name="see-also"></a>Consulte também  
 [Backup e Restauração de bancos de dados do SQL Server](../backup-restore/back-up-and-restore-of-sql-server-databases.md)   
 [Sobre o envio de logs &#40;SQL Server&#41;](../../database-engine/log-shipping/about-log-shipping-sql-server.md)  
  
  