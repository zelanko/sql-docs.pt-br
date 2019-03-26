---
title: Serviço Change Data Capture para Oracle da Attunity | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 22ec8a5c-9550-4d38-8a4a-485ec3e53ea8
author: janinezhang
ms.author: janinez
manager: craigg
ms.openlocfilehash: 3e24cb57b7bc9e0a5addbde4c0249448bb84e905
ms.sourcegitcommit: 7ccb8f28eafd79a1bddd523f71fe8b61c7634349
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 03/20/2019
ms.locfileid: "58290652"
---
# <a name="change-data-capture-service-for-oracle-by-attunity"></a>Serviço Change Data Capture para Oracle da Attunity
  O Serviço CDC para Oracle é um Serviço do Windows que examina os logs de transação do Oracle e capturam alterações a tabelas de interesse do Oracle em tabelas de alteração do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . As tabelas de alteração do SQL onde as alterações capturadas do Oracle são armazenadas são do mesmo tipo das tabelas de alteração usadas no recurso Change Data Capture nativo do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isto faz o consumo destas alterações tão fácil quanto consumir alterações feitas a bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] .  
  
## <a name="installation"></a>Instalação  
 O Microsoft® Change Data Capture Designer e Service para Oracle da Attunity para o Microsoft SQL Server® 2016 são parte do SQL Server 2016 Feature Pack. Baixe componentes do Feature Pack da [página da Web do SQL Server 2016 Feature Pack](https://go.microsoft.com/fwlink/?LinkId=746297).  
  
 O Serviço CDC para Oracle pode ser instalado em qualquer computador Windows com suporte com acesso a bancos de dados Oracle de origem que são capturados e a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino em que reside o banco de dados de CDC de destino. O Serviço CDC não precisa de uma instalação local do banco de dados Oracle ou o banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] , somente seus clientes com suporte. Para obter mais informações sobre onde instalar os componentes necessários do banco de dados, consulte a seção **Pré-requisitos de banco de dados** deste tópico.  
  
 A instalação do Serviço [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] CDC para Oracle coloca a interface de usuário da configuração de serviço e o programa de serviço no local selecionado. O Serviço CDC para Oracle é configurado separadamente usando o Console de Configuração do Serviço Oracle CDC. Para obter mais informações sobre como configurar o Serviço Oracle CDC, consulte [Ajuda F1 do serviço Change Data Capture para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md).  
  
 O Serviço CDC para Oracle pode ser instalado em qualquer computador Windows com suporte em que o [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client esteja instalado; ele não precisa estar instalado no mesmo computador em que o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino está instalado.  
  
## <a name="supported-windows-environments"></a>Ambientes de Windows com suporte  
 O Serviço Change Data Capture para Oracle da Attunity pode ser executado nos ambientes de Windows a seguir:  
  
-   Windows 8 e 8.1  
-   Windows 10  
-   Windows Server 2012 e 2012 R2
-   Windows Server 2016
  
## <a name="database-prerequisites"></a>Pré-requisitos de banco de dados  
 Para funcionar com o Serviço CDC para Oracle, você deverá instalar o software Oracle do [!INCLUDE[ssCurrent](../../includes/sscurrent-md.md)] Native Client. Este é um pré-requisito que deve ser obtido do Oracle e instalado antes de instalar o Serviço Oracle CDC. Além disso, você precisa instalar o Cliente ODBC do SQL Server usando a Instalação do SQL Server.  
  
 O Serviço CDC para Oracle dá suporte às seguintes versões:  
  
### <a name="source-oracle-database"></a>Banco de dados Oracle de origem  
  
-   Banco de dados Oracle 10g Versão 2
-   Banco de dados Oracle 11g Versão 1 e Versão 2
-   Oracle Database 12c em instalação clássica. (Não há suporte para a instalação multilocatária.)  
  
### <a name="target-sql-server-database"></a>Banco de Dados do SQL Server de destino  
 Para obter uma lista de recursos com suporte nas edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte [Recursos com suporte nas edições do SQL Server 2016](~/sql-server/editions-and-supported-features-for-sql-server-2016.md).  
  
## <a name="running-the-installation-program"></a>Executando o programa de instalação  
 Para instalar o Serviço CDC para Oracle, abra o assistente de instalação para a plataforma Windows que você está usando (32/64 bits) e siga as instruções na tela.  
  
## <a name="uninstalling-change-data-capture-service-for-oracle-by-attunity"></a>Desinstalando o Serviço Change Data Capture para Oracle da Attunity  
 É possível desinstalar o Serviço CDC para Oracle usando Painel de Controle, Programas e Recursos.  
  
 Desinstalar o Serviço CDC não exclui os bancos de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] criados. Para remoção completa da ferramenta, você deverá remover o banco de dados MSXDBCDC e os bancos de dados de CDC específicos que foram criados na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino com os quais você trabalhou.  
  
 Se você desinstalar o software Serviço CDC de um computador e instalá-lo em outro, só precisará fornecer as seguintes definições:  
  
-   Conta de serviço  
  
-   [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Cadeia de conexão e credenciais  
  
-   A senha mestra  
  
 Todas as outras definições são armazenadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e estão disponíveis da instalação anterior em outro computador.  
  
## <a name="in-this-documentation"></a>Nesta documentação  
  
-   [Arquitetura de sistema do Serviço Change Data Capture para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-system-architecture.md)  
  
-   [O Serviço Oracle CDC](../../integration-services/change-data-capture/the-oracle-cdc-service.md)  
  
-   [Ajuda F1 do serviço Change Data Capture para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-f1-help.md)  
  
-   [Guia de instruções do Serviço Change Data Capture para Oracle da Attunity](../../integration-services/change-data-capture/change-data-capture-service-for-oracle-by-attunity-how-to-guide.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Trabalhando com o serviço Oracle CDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
  
