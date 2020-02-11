---
title: Configurar SQL Server para receber cópias de tabelas remotas
description: Descreve como configurar uma instância de SQL Server do SMP externa para receber cópias de tabelas remotas de data warehouse paralelas.
author: mzaman1
ms.prod: sql
ms.technology: data-warehouse
ms.topic: conceptual
ms.date: 04/17/2018
ms.author: murshedz
ms.reviewer: martinle
ms.custom: seo-dt-2019
ms.openlocfilehash: 3e5475e86582ede2e6fa7ca5a302bba7ee74faa3
ms.sourcegitcommit: b87d36c46b39af8b929ad94ec707dee8800950f5
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 02/08/2020
ms.locfileid: "74401322"
---
# <a name="configure-an-external-smp-sql-server-to-receive-remote-table-copies---parallel-data-warehouse"></a>Configurar um SQL Server SMP externo para receber cópias de tabela remota-data warehouse paralelos
Descreve como configurar uma instância de SQL Server externa para receber cópias de tabelas remotas de data warehouse paralelas.  

Este tópico descreve uma das etapas de configuração para configurar a cópia de tabela remota. Para obter uma lista de todas as etapas de configuração, consulte [cópia da tabela remota](remote-table-copy.md).  
  
## <a name="before-you-begin"></a>Antes de começar  
Para poder configurar o SQL Server externo, você deve:  
  
-   Ter um sistema Windows com o SQL Server 2008 Enterprise Edition ou uma versão posterior pronta para ser instalado ou já instalado. O sistema do Windows já deve estar configurado de acordo com as instruções em [configurar um sistema externo do Windows para receber cópias de tabela remota usando InfiniBand](configure-an-external-windows-system-to-receive-remote-table-copies-using-infiniband.md).  
  
-   Uma conta do administrador do Windows com a capacidade de configurar a instância do SQL Server e o sistema do Windows.  
  
-   Uma conta de logon SQL Server (se SQL Server já estiver instalada) com a capacidade de criar logons e conceder permissões nos bancos de dados de destino.  
  
## <a name="HowToSQLServer"></a>Configurar um SQL Server SMP externo para receber cópias de tabelas remotas  
O recurso de cópia de tabela remota copia tabelas do dispositivo SQL Server PDW para um banco de dados SMP SQL Server que está sendo executado em um sistema Windows. Depois de configurar o sistema externo do Windows para receber cópias de tabelas remotas, a próxima etapa é instalar e configurar o SQL Server no sistema Windows.  
  
Para configurar SQL Server, use as seguintes etapas:  
  
1.  Instale o SQL Server 2008 Enterprise Edition ou uma versão posterior no sistema Windows. Isso é conhecido como o SQL Server SMP.  
  
2.  Configure SQL Server para aceitar conexões TCP/IP em uma porta TCP fixa. Essa configuração é desabilitada por padrão e deve ser habilitada para permitir que SQL Server PDW se conectem ao SQL Server SMP.  
  
3.  Desabilite o Firewall do Windows ou configure a porta TCP do SMP SQL Server para que ela funcione com o Firewall do Windows habilitado.  
  
4.  Configure SQL Server para permitir SQL Server modo de autenticação. A exportação de dados paralelo sempre usa contas de SQL Server para autenticação.  
  
5.  Determine uma conta de SQL Server no SQL Server SMP que será usado para autenticação. Conceda a essa conta o privilégio para criar, remover e inserir dados em tabelas no banco de dados de destino para a operação de exportação de dados paralelos.  
  
## <a name="BPSQLConfig"></a>Práticas recomendadas para a configuração de SQL Server SMP para cópia de tabela remota  
Ao configurar o SQL Server SMP para receber cópias de tabela remota, use as práticas recomendadas a seguir para melhorar o desempenho.  
  
1.  Siga as práticas recomendadas, conforme documentado em SQL Server documentação do produto. Por exemplo, habilite a criptografia de dados. Para obter mais informações sobre como proteger SQL Server, consulte [protegendo SQL Server](../relational-databases/security/securing-sql-server.md) no msdn.  
  
2.  Use o modelo de recuperação bulk-logged ou simples.  
  
    Durante as operações de exportação de dados paralelos, os dados são inseridos em massa na tabela de destino recém-criada. Para obter o desempenho máximo durante a inserção em massa, defina o banco de dados de destino para usar o modelo de recuperação bulk-logged ou Simple.  
  
3.  Use a opção batch_size para recuperar o espaço de log.  
  
    Embora os modelos de recuperação bulk-logged ou simples usem o log mínimo para os dados inseridos em massa, algum log ainda ocorrerá. Para evitar que os arquivos de log cresçam muito grandes, use a opção SQL Server batch_size para recuperar periodicamente o espaço de log.  
  
<!-- MISSING LINKS 
## See Also  
[Common Metadata Query Examples &#40;SQL Server PDW&#41;](../sqlpdw/common-metadata-query-examples-sql-server-pdw.md)  
-->
  
