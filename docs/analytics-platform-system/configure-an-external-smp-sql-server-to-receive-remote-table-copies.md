---
title: "Configurar servidor de SQL SMP externos para receber cópias da tabela remota (PDW)"
author: barbkess
ms.author: barbkess
manager: jhubbard
ms.prod: sql-non-specified
ms.prod_service: mpp-data-warehouse
ms.service: 
ms.component: analytics-platform-system
ms.technology: mpp-data-warehouse
ms.custom: 
ms.date: 01/13/2017
ms.reviewer: na
ms.suite: sql
ms.tgt_pltfrm: na
ms.topic: article
ms.assetid: 6bbd2ed6-064e-4b45-b67b-608dc0f2b2bc
caps.latest.revision: "13"
ms.openlocfilehash: 56ef4d9b75e8051a17c276556a321ed19ddcf2d8
ms.sourcegitcommit: 44cd5c651488b5296fb679f6d43f50d068339a27
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 11/17/2017
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies"></a>Configurar um servidor SQL SMP externos para receber cópias da tabela remota
Descreve como configurar uma instância externa do SQL Server para receber cópias da tabela remota do SQL Server PDW.  
  
Este tópico descreve uma das etapas de configuração para configurar a cópia da tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Antes de configurar o SQL Server externa, você deve:  
  
-   Ter um sistema Windows com o SQL Server 2008 Enterprise Edition ou uma versão posterior pronta para ser instalado ou já está instalado. O sistema do Windows já deve estar configurado de acordo com as instruções em [configurar um externo Windows System para recebimento remoto tabela cópias usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Uma conta de administrador do Windows com a capacidade de configurar a instância do SQL Server e o sistema do Windows.  
  
-   Uma conta do SQL Server logon (se o SQL Server já estiver instalado) com a capacidade de criar logons e conceder permissões nos bancos de dados de destino.  
  
## <a name="HowToSQLServer"></a>Configurar um servidor SQL SMP externos para receber cópias da tabela remota  
O recurso de cópia da tabela remota copia as tabelas do dispositivo PDW do SQL Server para um banco de dados externo do SMP SQL Server está em execução em um sistema Windows. Depois de configurar o sistema externo do Windows para receber cópias da tabela remota, a próxima etapa é instalar e configurar o SQL Server para o sistema do Windows.  
  
Para configurar o SQL Server, use as seguintes etapas:  
  
1.  Instale o SQL Server 2008 Enterprise Edition ou uma versão posterior do sistema do Windows. Isso é chamado de SMP SQL Server.  
  
2.  Configure o SQL Server para aceitar conexões TCP/IP em uma porta TCP fixa. Essa configuração é desabilitada por padrão e deve ser habilitada para permitir que o SQL Server PDW para se conectar ao SQL Server SMP.  
  
3.  Desabilite o firewall do Windows ou configure a porta TCP do SQL Server do SMP para que ele funcione com o firewall do Windows habilitado.  
  
4.  Configure o SQL Server para permitir que o modo de autenticação do SQL Server. Os dados em paralelo exportar sempre usa contas do SQL Server para autenticação.  
  
5.  Determine uma conta do SQL Server no SQL Server SMP que será usado para autenticação. Conceda o privilégio para criar, remover e inserir dados em tabelas no banco de dados de destino para a operação de exportação de dados em paralelo à conta.  
  
## <a name="BPSQLConfig"></a>Práticas recomendadas para configuração do servidor SQL de SMP de cópia da tabela remota  
Ao configurar o SQL Server de SMP para receber cópias da tabela remota, use as seguintes práticas recomendadas para melhorar o desempenho.  
  
1.  Siga as práticas recomendadas, conforme documentado na documentação de produto do SQL Server. Por exemplo, habilite a criptografia de dados. Para obter mais informações sobre como proteger o SQL Server, consulte [protegendo o SQL Server](../relational-databases/security/securing-sql-server.md) no MSDN.  
  
2.  Use o modelo de recuperação bulk-logged ou simples.  
  
    Operações de exportação durante os dados em paralelo, dados são inserida na tabela de destino recém-criada em massa. Para obter desempenho máximo durante a inserção em massa, defina o banco de dados de destino para usar bulk-logged ou o modelo de recuperação simples.  
  
3.  Use a opção batch_size para recuperar o espaço de log.  
  
    Embora o uso mínimo de registro em log para os dados em massa inserido de modelos de recuperação bulk-logged ou simple, alguns log ainda ocorre. Para impedir que os arquivos de log fique muito grande, use a opção de batch_size do SQL Server para recuperar periodicamente o espaço de log.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
