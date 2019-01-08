---
title: Arquitetura de sistema do serviço Change Data Capture para Oracle da Attunity | Microsoft Docs
ms.custom: ''
ms.date: 03/06/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 1db6c737-3c60-4066-a0a3-3611e1c83e4e
author: douglaslMS
ms.author: douglasl
manager: craigg
ms.openlocfilehash: e04a6a174143d2da6d85ae27dd84ecf516f533fa
ms.sourcegitcommit: ceb7e1b9e29e02bb0c6ca400a36e0fa9cf010fca
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 12/03/2018
ms.locfileid: "52756871"
---
# <a name="change-data-capture-service-for-oracle-by-attunity-system-architecture"></a>Arquitetura de sistema do Serviço Change Data Capture para Oracle da Attunity
  O Serviço CDC para Oracle captura alterações feitas em tabelas selecionadas em um ou mais bancos de dados Oracle de origem em bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC localizados em uma instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] . O diagrama a seguir mostra os componentes que compõem o Serviço CDC para Oracle.  
  
 ![Arquitetura de Serviço](../media/service-architecture.gif "Arquitetura de Serviço")  
  
 Esta figura ilustra quatro plataformas que são usadas. Em muitos casos, estas plataformas podem se sobrepor, porém este diagrama representa um caso de uso padrão. Por exemplo, faz sentido que os bancos de dados Oracle e [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] sejam executados em um computador separado e não sejam compartilhados com a plataforma do Serviço Oracle CDC ou a plataforma da qual o Serviço CDC é criado. As plataformas ilustradas nesta figura são:  
  
-   O serviço Oracle CDC: Isso pode ser qualquer computador Windows com suporte onde o serviço Oracle CDC está instalado e executado. Esta plataforma também pode representar um nó de cluster em um cluster de failover da Microsoft (as configurações de alta disponibilidade são discutidas posteriormente neste documento).  
  
-   O banco de dados Oracle: Isso pode ser qualquer computador em que uma versão com suporte do banco de dados Oracle é executado. Isto inclui qualquer computador que execute Windows, Linux ou qualquer outro sistema operacional com suporte pela versão do banco de dados Oracle instalado. Observe que o diagrama mostra esta plataforma no plural porque um único Serviço Oracle CDC pode capturar alterações de vários bancos de dados Oracle de origem.  
  
-   O [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]: Isso pode ser qualquer computador em que o destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados (um SKU com suporte de [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]) é executado. Um Serviço Oracle CDC dá suporte a um destino do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] em que ele armazena tabelas de alteração e configuração de serviço. A Plataforma do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] também pode representar uma instância clusterizada do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] ou uma instância espelhada do [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)] usando o recurso **AlwaysOn** .  
  
-   O Designer do Oracle CDC: Isso pode ser qualquer computador Windows com suporte que pode acessar o banco de dados do Oracle de origem e destino [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] banco de dados.  
  
 A tabela a seguir descreve os componentes que são executados nas quatro plataformas descritas acima.  
  
|Componente/descrição|O componente é composto de:|  
|----------------------------|----------------------------|  
|Serviço Oracle CDC: Isso é um serviço do Windows onde ocorre a atividade de captura de dados de alteração.|Instância Oracle CDC: Um subprocesso do serviço Oracle CDC que trata alterações de atividade de captura de dados para um banco de dados do Oracle de origem única (há uma instância do Oracle CDC por banco de dados de origem Oracle).<br /><br /> Leitor de Log do Oracle: Lê logs de transação do Oracle usando o cliente Oracle.<br /><br /> Cliente Oracle: O Oracle Instant Client usado para comunicação com a Oracle. Este é um pré-requisito que deve ser obtido do Oracle e instalado antes de instalar o Serviço Oracle CDC.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Gravador de alteração: Isso grava alterações confirmadas feitas na tabela Oracle capturada em [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]nas tabelas de alteração. Este componente também mantém esse estado de captura dentro do banco de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino.<br /><br /> [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)]Cliente ODBC: O cliente Microsoft Native para [!INCLUDE[ssCurrent](../../../includes/sscurrent-md.md)]. Este é um componente de pré-requisito que deve ser obtido da Microsoft e instalado antes de instalar o Serviço Oracle CDC.|  
|Configuração do serviço de CDC Oracle: Isso é um snap-in do Console de gerenciamento Microsoft que cria o serviço do Windows e define sua configuração.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cliente: O cliente do SQL ADO.NET que é fornecido com a versão 4 do .NET framework.|  
|Banco de dados Oracle: Um banco de dados do Oracle de origem do quais as alterações para selecionar tabelas são capturadas.|Minerador de logs: Um componente do Oracle por meio do qual os logs de transação do Oracle são lidos.<br /><br /> Logs de transação: O online e arquivados Oracle Refazer Logs que são usados pela Oracle para garantir que o banco de dados poderão ser revertidas transações e recuperar de falhas (neste caso, o Oracle no banco de dados deve operar em modo de log de arquivo morto).|  
|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Instância: Um [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância em que os bancos de dados CDC são hospedados. Isso pode ser uma Instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] clusterizada (cluster de failover) ou um banco de dados espelhado (AlwaysOn).|O banco de dados MSXDBCDC: Um banco de dados em que informações sobre os serviços CDC trabalha com este [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] instância é mantida. Também mantém informações sobre as Instâncias Oracle CDC tratadas por cada Serviço CDC. Este banco de dados é criado como parte do processo de criação do Serviço CDC.<br /><br /> Os bancos de dados CDC: bancos de dados do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] que armazenam as alterações feitas a um dos bancos de dados Oracle de origem. Os bancos de dados CDC são habilitados para o [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC para que tenham tabelas e funções do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] CDC, facilitando consumir alterações que se originam do Oracle.|  
|Designer do Oracle CDC: Um snap-in do Console de gerenciamento Microsoft que ajuda a criar instâncias Oracle CDC. Use isto para selecionar as tabelas e colunas a serem capturadas, forneça informações de conexão do Oracle e gerencie o ciclo de vida de Instâncias CDC.|[!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] Cliente: O cliente do SQL ADO.NET que é fornecido com a versão 4 do .NET framework.<br /><br /> Cliente Oracle: O Oracle Instant Client usado para comunicação com a Oracle. Este é um componente de pré-requisito que deve ser obtido da Oracle e instalado antes de instalar o Serviço Oracle CDC.|  
  
 O Serviço Oracle CDC e suas Instâncias Oracle CDC filhas só podem se comunicar com o banco de dados Oracle de origem e a instância do [!INCLUDE[ssNoVersion](../../../includes/ssnoversion-md.md)] de destino como clientes. Eles não escutam ativamente em nenhuma rede e outros protocolos. O Serviço Oracle CDC monitora os bancos de dados CDC em busca de alterações de configuração e atualiza sua operação com base na configuração atualizada.  
  
  
