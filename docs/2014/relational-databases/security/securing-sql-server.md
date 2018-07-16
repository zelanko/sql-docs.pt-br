---
title: Protegendo o SQL Server | Microsoft Docs
ms.custom: ''
ms.date: 06/13/2017
ms.prod: sql-server-2014
ms.reviewer: ''
ms.suite: ''
ms.technology: security
ms.tgt_pltfrm: ''
ms.topic: conceptual
f1_keywords:
- Security [SQL Server]
helpviewer_keywords:
- database objects [SQL Server], security
- SQL Server, security
- operating systems [SQL Server], security
- security [SQL Server], planning
- applications [SQL Server], security
ms.assetid: 4d93489e-e9bb-45b3-8354-21f58209965d
caps.latest.revision: 28
author: edmacauley
ms.author: edmaca
manager: craigg
ms.openlocfilehash: 4b3b01893519137c5fb707e9cd6b9dad7366c3bf
ms.sourcegitcommit: c18fadce27f330e1d4f36549414e5c84ba2f46c2
ms.translationtype: MT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/02/2018
ms.locfileid: "37250086"
---
# <a name="securing-sql-server"></a>Protegendo o SQL Server
  A segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] pode ser exibida como uma série de etapas, envolvendo quatro áreas: a plataforma, a autenticação, os objetos (inclusive os dados) e os aplicativos que acessam o sistema. Os tópicos a seguir guiarão você pela criação e implementação de um plano de segurança efetivo.  
  
 Você pode encontrar mais informações sobre a segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] no site do [SQL Server](http://go.microsoft.com/fwlink/?LinkID=31629) . Ele inclui um guia de práticas recomendadas e uma lista de verificação de segurança. Este site também contém as informações mais recentes de service packs e downloads.  
  
## <a name="platform-and-network-security"></a>Segurança de rede e plataforma  
 A plataforma do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui hardware físico e sistemas de redes que conectam os clientes aos servidores de banco de dados e os arquivos binários que são usados para processar solicitações do banco de dados.  
  
### <a name="physical-security"></a>Segurança física  
 As práticas recomendadas para segurança física limitam estritamente o acesso ao servidor físico e aos componentes de hardware. Por exemplo, o uso de espaços bloqueados com acesso restrito para o hardware do servidor de banco de dados e dispositivos da rede. Além disso, limite o acesso à mídia de backup armazenando-a em local seguro fora do ambiente de trabalho.  
  
 A implementação da segurança de rede física começa mantendo usuários não autorizados afastados da rede. A tabela a seguir contém mais informações sobre a segurança de rede.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] e acesso de rede para outras edições do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|"Configurando e oferecendo segurança ao ambiente de servidor" nos Manuais Online do [!INCLUDE[ssEW](../../includes/ssew-md.md)]|  
  
### <a name="operating-system-security"></a>Segurança do sistema operacional  
 Os service packs e atualizações do sistema operacional incluem aperfeiçoamentos de segurança importantes. Aplique todas as atualizações ao sistema operacional depois de testá-las com os aplicativos do banco de dados.  
  
 Os firewalls também fornecem formas efetivas para implementar a segurança. Logicamente, um firewall é o responsável por separar ou restringir o tráfego da rede, que pode ser configurado para aplicar a política de segurança de dados de sua empresa. Se você usa um firewall, aumenta a segurança no nível do sistema operacional, criando um gargalo que permite o foco nas medidas de segurança. A tabela a seguir contém mais informações sobre como usar um firewall com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Configurando um firewall para trabalhar com [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Configurar um Firewall do Windows para acesso ao Mecanismo de Banco de Dados](../../database-engine/configure-windows/configure-a-windows-firewall-for-database-engine-access.md)|  
|Configurando um firewall para trabalhar com [!INCLUDE[ssISnoversion](../../includes/ssisnoversion-md.md)]|[Configurar um Firewall do Windows para acesso ao serviço SSIS](../../integration-services/configure-a-windows-firewall-for-access-to-the-ssis-service.md)|  
|Configurando um firewall para trabalhar com [!INCLUDE[ssASnoversion](../../includes/ssasnoversion-md.md)]|[Configurar o Firewall do Windows para permitir o acesso ao Analysis Services](../../analysis-services/instances/configure-the-windows-firewall-to-allow-analysis-services-access.md)|  
|Abrindo portas específicas em um firewall para habilitar o acesso ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Configurar o Firewall do Windows para permitir acesso ao SQL Server](../../sql-server/install/configure-the-windows-firewall-to-allow-sql-server-access.md)|  
|Configurando suporte à Proteção Estendida para Autenticação usando associação de canal e associação de serviço|[Conectar-se ao mecanismo de banco de dados usando proteção estendida](../../database-engine/configure-windows/connect-to-the-database-engine-using-extended-protection.md)|  
  
 A redução da área de superfície é uma medida de segurança que envolve a interrupção ou desabilitação de componentes não utilizados. Essa redução auxilia na melhoria da segurança, fornecendo menos vias para possíveis ataques em um sistema. A chave para limitar a área da superfície do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] inclui a execução de serviços necessários que possuem "privilégios mínimos", concedendo apenas os direitos adequados aos serviços e usuários. A tabela a seguir contém mais informações sobre o acesso ao sistema e aos serviços.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Serviços requeridos para [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Configurar contas de serviço e permissões do Windows](../../database-engine/configure-windows/configure-windows-service-accounts-and-permissions.md)|  
  
 Se seu sistema [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usar o IIS (Serviços de Informações da Internet), etapas adicionais serão necessárias para auxiliar na proteção da superfície da plataforma. A tabela a seguir contém informações sobre o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e os Serviços de Informações da Internet.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Segurança do IIS com [!INCLUDE[ssEW](../../includes/ssew-md.md)]|"Segurança do IIS" nos Manuais Online do [!INCLUDE[ssEW](../../includes/ssew-md.md)]|  
|[!INCLUDE[ssRSnoversion](../../includes/ssrsnoversion-md.md)] Autenticação|[Autenticação no Reporting Services](../../reporting-services/extensions/security-extension/authentication-in-reporting-services.md)|  
|[!INCLUDE[ssEW](../../includes/ssew-md.md)] e acesso ao IIS|"Fluxograma de segurança dos Serviços de Informações da Internet" nos Manuais Online do [!INCLUDE[ssEW](../../includes/ssew-md.md)]|  
  
### <a name="sql-server-operating-system-files-security"></a>Segurança dos arquivos do sistema operacional do SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] usa arquivos do sistema operacional para operação e armazenamento de dados. As práticas recomendadas para a segurança de arquivos exigem que você restrinja o acesso a esses arquivos. A tabela a seguir contém informações sobre esses arquivos.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] arquivos de programa|[Locais de arquivos para instâncias padrão e nomeadas do SQL Server](../../sql-server/install/file-locations-for-default-and-named-instances-of-sql-server.md)|  
  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Os service packs e as atualizações fornecem segurança avançada. Para determinar o último service pack disponível para o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], consulte o site [SQL Server](http://go.microsoft.com/fwlink/?LinkID=31629) .  
  
 Você pode usar o script a seguir para determinar o service pack instalado no sistema.  
  
```  
SELECT CONVERT(char(20), SERVERPROPERTY('productlevel'));  
GO  
```  
  
## <a name="principals-and-database-object-security"></a>Segurança de entidades e objetos do banco de dados  
 Entidades são acessos de indivíduos, grupos e processos concedidos ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]. "Protegíveis" são servidores, bancos de dados e objetos que o banco de dados contém. Cada um tem um conjunto de permissões que pode ser configurado para ajudar a reduzir a área da superfície do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . A tabela a seguir contém informações sobre entidades e protegíveis.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Usuários, funções e processos do servidor e do banco de dados|[Entidades &#40;Mecanismo de Banco de Dados&#41;](authentication-access/principals-database-engine.md)|  
|Segurança de objetos do servidor e do banco de dados|[Protegíveis](securables.md)|  
|A hierarquia de segurança do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Hierarquia de permissões &#40;Mecanismo de Banco de Dados&#41;](permissions-hierarchy-database-engine.md)|  
  
### <a name="encryption-and-certificates"></a>Criptografia e certificados  
 A criptografia não resolve problemas de controle de acesso. Porém, aumenta a segurança, limitando a perda de dados mesmo se os controles de acesso forem ignorados, o que é raro. Por exemplo, se o computador host do banco de dados for malconfigurado e um usuário malicioso obtiver dados confidenciais, como números de cartão de crédito, essas informações roubadas poderão ser inúteis se estiverem criptografadas. A tabela seguinte contém mais informações sobre criptografia no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|A hierarquia de criptografia no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Hierarquia de criptografia](encryption/encryption-hierarchy.md)|  
|Implementando conexões seguras|[Habilitar conexões criptografadas no Mecanismo de Banco de Dados &#40;SQL Server Configuration Manager&#41;](../../database-engine/configure-windows/enable-encrypted-connections-to-the-database-engine.md)|  
|Funções de criptografia|[Funções criptográficas &#40;Transact-SQL&#41;](/sql/t-sql/functions/cryptographic-functions-transact-sql)|  
  
 Os certificados são "chaves" de software compartilhadas entre dois servidores que ativam comunicações seguras por meio da autenticação segura. Você pode criar e usar certificados no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para aumentar a segurança de conexão e de objetos. A tabela a seguir contém informações sobre como usar certificados com o [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)].  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Criando um certificado para uso pelo [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[CREATE CERTIFICATE &#40;Transact-SQL&#41;](/sql/t-sql/statements/create-certificate-transact-sql)|  
|Usando um certificado com espelhamento de banco de dados|[Usar certificados para um ponto de extremidade de espelhamento de banco de dados &#40;Transact-SQL&#41;](../../database-engine/database-mirroring/use-certificates-for-a-database-mirroring-endpoint-transact-sql.md)|  
  
## <a name="application-security"></a>Segurança do aplicativo  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] As práticas recomendadas de segurança incluem a criação de aplicativos cliente seguros.  
  
 Para obter mais informações sobre como ajudar a proteger aplicativos cliente na camada de rede, consulte [Configuração de Rede Cliente](../../database-engine/configure-windows/client-network-configuration.md).  
  
## <a name="sql-server-security-tools-utilities-views-and-functions"></a>Ferramentas de segurança, utilitários, exibições e funções do SQL Server  
 [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] fornece ferramentas, utilitários, exibições e funções que podem ser usados para configurar e administrar a segurança.  
  
### <a name="sql-server-security-tools-and-utilities"></a>Ferramentas de segurança e utilitários do SQL Server  
 A tabela a seguir contém informações sobre as ferramentas e os utilitários do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] que você pode usar para configurar e administrar a segurança.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|Conexão, configuração e controle [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[Usar o SQL Server Management Studio](../../database-engine/use-sql-server-management-studio.md)|  
|Conectando-se ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e executando consultas no prompt de comandos|[Utilitário sqlcmd](../../tools/sqlcmd-utility.md)|  
|Configuração e controle de rede do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)]|[SQL Server Configuration Manager](../sql-server-configuration-manager.md)|  
|Habilitando e desabilitando recursos usando Gerenciamento Baseado em Políticas|[Administrar servidores com Gerenciamento Baseado em Políticas](../policy-based-management/administer-servers-by-using-policy-based-management.md)|  
|Manipulando chaves simétricas para um servidor de relatório|[Utilitário rskeymgmt &#40;SSRS&#41;](../../reporting-services/tools/rskeymgmt-utility-ssrs.md)|  
  
### <a name="sql-server-security-catalog-views-and-functions"></a>Exibições e funções do catálogo de segurança do SQL Server  
 O [!INCLUDE[ssDE](../../includes/ssde-md.md)] mostra informações de segurança em várias exibições e funções que são aperfeiçoadas para desempenho e utilitário. A tabela a seguir contém informações sobre as exibições e funções de segurança.  
  
|Para obter informações sobre|Consulte|  
|---------------------------|---------|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Exibições do catálogo de segurança que retornam informações sobre permissões, entidades, funções, etc, de nível de servidor e banco de dados. Além disso, há exibições do catálogo que fornecem informações sobre chaves de criptografia, certificados e credenciais.|[Exibições de catálogo de segurança &#40;Transact-SQL&#41;](/sql/relational-databases/system-catalog-views/security-catalog-views-transact-sql)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Funções de segurança que retornam informações sobre o usuário atual, permissões e esquemas.|[Funções de segurança &#40;Transact-SQL&#41;](/sql/t-sql/functions/security-functions-transact-sql)|  
|[!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] Exibições de gerenciamento dinâmico de segurança.|[Funções e exibições de gerenciamento dinâmico relacionadas à segurança &#40;Transact-SQL&#41;](/sql/relational-databases/system-dynamic-management-views/security-related-dynamic-management-views-and-functions-transact-sql)|  
  
## <a name="related-content"></a>Conteúdo relacionado  
 [Considerações sobre segurança para uma instalação do SQL Server](../../sql-server/install/security-considerations-for-a-sql-server-installation.md)  
  
 [Central de segurança do Mecanismo de Banco de Dados do SQL Server e Banco de Dados SQL do Azure](security-center-for-sql-server-database-engine-and-azure-sql-database.md)  
  
  
