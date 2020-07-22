---
title: O serviço Oracle CDC | Microsoft Docs
ms.custom: ''
ms.date: 03/14/2017
ms.prod: sql
ms.prod_service: integration-services
ms.reviewer: ''
ms.technology: integration-services
ms.topic: conceptual
ms.assetid: 47759ddc-358d-405b-acb9-189ada76ea6d
author: chugugrace
ms.author: chugu
ms.openlocfilehash: 95dc655d8c1ac23df7cbb058cba2c5c7f4e41419
ms.sourcegitcommit: c8e1553ff3fdf295e8dc6ce30d1c454d6fde8088
ms.translationtype: HT
ms.contentlocale: pt-BR
ms.lasthandoff: 07/22/2020
ms.locfileid: "86913966"
---
# <a name="the-oracle-cdc-service"></a>O Serviço Oracle CDC

[!INCLUDE[sqlserver-ssis](../../includes/applies-to-version/sqlserver-ssis.md)]


  O Serviço Oracle CDC é um serviço do Windows que executa o programa xdbcdcsvc.exe. O Serviço Oracle CDC pode ser configurado para executar vários Serviços do Windows no mesmo computador, cada um com um nome de serviços do Windows diferente. Criar diversos serviços do Windows do Oracle CDC em um único computador geralmente é feito para obter uma separação melhor entre eles, ou quando cada um precisa trabalhar com uma instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] diferente.  
  
 Um Serviço Oracle CDC é criado usando o console de Configuração do Serviço Oracle CDC ou é definido por meio da interface de linha de comando criada no programa xdbcdcsvc.exe. Em ambos os casos, cada Serviço Oracle CDC criado está associado a uma única instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] (que pode ser agrupada ou espelhada com a instalação do **AlwaysOn** ) e as informações de conexão (cadeia de conexão e credenciais de acesso) fazem parte da configuração do serviço.  
  
 Quando um Serviço Oracle CDC é iniciado, ele tenta se conectar à instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] com a qual está associado, obtém a lista de instâncias do Oracle CDC que precisa tratar e executa uma validação inicial de ambiente. Os erros durante a inicialização de serviço e qualquer informação de iniciar/parar são gravados no log de eventos de aplicativo do Windows. Quando uma conexão ao [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] é estabelecida, todos os erros e as mensagens de informações são gravadas na tabela **dbo.xdbcdc_trace** no banco de dados MSXDBCDC da instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Uma das verificações feitas durante a inicialização é a verificação de que nenhum outro Serviço Oracle CDC com o mesmo nome está funcionando atualmente. Se um serviço com o mesmo nome estiver conectado atualmente de um computador diferente, o Serviço Oracle CDC inserirá um loop de espera, aguardando que o outro serviço se desconecte antes de continuar a tratar o trabalho do Oracle CDC.  
  
 Quando o Serviço Oracle CDC passa todas as verificações de inicialização, ele verifica a tabela **dbo.xdbcdc_databases** no banco de dados MSXDBCDC em busca de todas as Instâncias Oracle CDC habilitadas. Para cada Instância Oracle CDC habilitada, o serviço inicia um subprocesso para tratar essa Instância Oracle CDC.  
  
 Quando uma Instância Oracle CDC inicia, ela acessa o banco de dados do SQL Server CDC com o mesmo nome que a Instância CDC e recupera seu estado da execução anterior. Ela também verifica se tudo está sendo executado corretamente. Em seguida, é retomado o processamento de alterações, a leitura dos logs de transação do Oracle e a gravação de alterações no banco de dados CDC.  
  
 O Serviço Oracle CDC monitora periodicamente a tabela **dbo.xdbcdc_tables** no banco de dados MSXDBCDC para determinar se houve alterações de configuração às configurações da Instância Oracle CDC. Se uma alteração for localizada, o Serviço Oracle CDC notificará a Instância Oracle CDC de que é preciso verificar se há alterações em sua configuração. A maioria das alterações de configuração, como adicionar e remover instâncias de captura, pode ser aplicada enquanto a instância do Oracle CDC está habilitada, outras exigem que a Instância Oracle CDC seja reiniciada.  
  
 Ao usar o console de Designer Oracle CDC, as alterações são automaticamente detectadas. Ao atualizar a configuração do Oracle CDC usando SQL diretamente, o procedimento a seguir deve ser chamado para que o Serviço Oracle CDC perceba a alteração de configuração:  
  
```sql
DECLARE @dbname nvarchar(128) = 'HRcdc'  
EXECUTE [MSXDBCDC].[dbo].[xdbcdc_update_config_version] @dbname  
GO  
  
```  
  
 O processo da Instância Oracle CDC atualiza seu status na tabela do sistema **cdc.xdbcdc_state** e grava informações de erro na tabela **cdc.xdbcdc_trace** . A tabela **xdbcdc_state** é útil para monitorar o estado da Instância Oracle CDC. Ela fornece o status atualizado, vários contadores (como número de alterações lidas do Oracle, número de alterações gravadas no [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)], número de transação confirmada gravada e o número atual de transações em andamento), bem como indicação de latência.  
  
 A configuração da Instância Oracle CDC é salva na tabela **cdc.xdbcdc_config** , que é a tabela com a qual o console de Designer do Oracle CDC trabalha. Como a configuração inteira de uma Instância Oracle CDC está localizada na instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] de destino e nos bancos de dados CDC, é possível criar scripts de implantação do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] para uma Instância Oracle CDC. Isto é feito usando os consoles de Configuração de Serviço Oracle CDC e Designer Oracle CDC.  
  
## <a name="security-considerations"></a>Considerações de segurança  
 Veja a seguir a descrição dos requisitos de segurança necessários para trabalhar com o Serviço CDC para Oracle.  
  
### <a name="protection-of-source-oracle-data"></a>Proteção dos dados do Oracle de origem  
 O serviço Oracle CDC não exige acesso a dados de origem do Oracle e está protegido porque garante que as credenciais da mineração de logs não deem permissão SELECT a tabelas de cliente Oracle.  
  
### <a name="protection-of-source-oracle-change-data"></a>Proteção dos dados de alteração do Oracle de origem  
 O serviço Oracle CDC é fornecido com credenciais de mineração de logs que permitem que o serviço capture alterações feitas a qualquer tabela no banco de dados Oracle. Os dados de alteração não têm as permissões de acesso granulares que as tabelas regulares, de modo que o acesso a dados de alteração ignora os controles internos de acesso a dados do Oracle.  
  
 As tabelas de origem capturadas do Oracle têm tabelas de espelho vazias com os mesmos nome de esquema e tabela no banco de dados CDC. Os dados capturados estão armazenados em instâncias de captura do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] e oferecem a mesma proteção fornecida para alterações capturadas do banco de dados do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Para obter acesso aos dados de alteração associados a uma instância de captura, o usuário deve ter acesso de seleção a todas as colunas capturadas da tabela de espelho associada. Além disso, se uma função de acesso for especificada quando a instância de captura for criada, o chamador também deverá ser um membro da função de acesso especificada. Outras funções gerais de captura de dados de alteração para o acesso aos metadados estão acessíveis a todos os usuários de banco de dados por meio da função pública, embora o acesso aos metadados retornados também seja geralmente concedido pelo uso do acesso de seleção às tabelas de origem subjacentes e pela associação em qualquer função associada definida.  
  
 Isto significa que os usuários com a função de servidor fixa **sysadmin** ou a função de banco de dados fixa **db_owner** têm (por padrão) acesso completo aos dados capturados; além disso, acesso adicional pode ser concedido por meio funções associadas ou pela concessão de acesso Select às colunas capturadas.  
  
### <a name="protection-of-source-oracle-log-mining-credentials"></a>Proteção de credenciais de mineração de logs do Oracle de origem  
 A configuração do serviço Oracle CDC, armazenada no banco de dados CDC (na tabela cdc.xdbcdc_config) inclui o nome de usuário de mineração de logs e sua senha associada.  
  
 A senha de mineração de logs é armazenada criptografada por meio de uma chave assimétrica com o nome fixo `xdbcdc_asym_key` que é criado automaticamente com o comando a seguir:  
  
```sql
USE [<cdc-database-name>]  
CREATE ASYMMETRIC KEY xdbcdc_asym_key  
    WITH ALGORITHM = RSA_1024  
    ENCRYPTION BY PASSWORD = '<cdc-database-name><asym-key-password>'  
  
```  
  
 Se um algoritmo diferente for usado, esta chave poderá ser removida e uma nova de mesmo nome e criptografada pela mesma senha poderá ser criada.  
  
 A senha da chave assimétrica é a senha mestra salva no Registro no caminho **HKLM\Software\Microsoft\XDBCDCSVC\\<service-name>** . Essa chave só está acessível para administradores locais e para a conta de serviço do Windows do Oracle CDC. A chave contém um valor binário **AsymmetricKeyPassword** criptografado que armazenou a senha da chave assimétrica. O acesso a esta chave do Registro é necessário para poder acessar as credenciais de mineração de logs do Oracle.  
  
 Para usar a cláusula ENCRYPTION BY PASSWORD, a senha deverá atender os requisitos de política de senha do Windows para o computador que está executando a instância do [!INCLUDE[ssNoVersion](../../includes/ssnoversion-md.md)] . Isto é feito selecionando a senha da chave assimétrica de acordo com essa política.  
  
 Se a senha de chave assimétrica for perdida, as credenciais de mineração de logs para cada instância Oracle CDC devem ser especificadas novamente no Designer de Serviço Oracle CDC.  
  
 A chave assimétrica é criada automaticamente no banco de dados CDC quando o serviço CDC detecta um banco de dados CDC da instância Oracle que não tem esta chave assimétrica ou quando a chave existe, mas a senha não corresponde.  
  
### <a name="oracle-cdc-service-windows-service-account"></a>Conta de serviço do Windows do Serviço Oracle CDC  
 A conta de serviço usada com o serviço do Windows do Oracle CDC não exige nenhum privilégio adicional. Esta conta deve poder usar a API do Oracle Native Client e a API ODBC do SQL Server Native Client. Ela também precisa poder acessar a chave de configuração de serviço no Registro (este console de Configuração do Serviço CDC configura o ACL para isso).  
  
## <a name="in-this-section"></a>Nesta seção  
  
-   [Suporte de alta disponibilidade](../../integration-services/change-data-capture/high-availability-support.md)  
  
-   [Permissões necessárias para conexão do SQL Server para o Serviço CDC](../../integration-services/change-data-capture/sql-server-connection-required-permissions-for-the-cdc-service.md)  
  
-   [Funções de usuário](../../integration-services/change-data-capture/user-roles.md)  
  
-   [Trabalhando com o serviço Oracle CDC](../../integration-services/change-data-capture/working-with-the-oracle-cdc-service.md)  
  
## <a name="see-also"></a>Consulte Também  
 [Como gerenciar um serviço CDC local](../../integration-services/change-data-capture/how-to-manage-a-local-cdc-service.md)   
 [Gerenciar um serviço Oracle CDC](../../integration-services/change-data-capture/manage-an-oracle-cdc-service.md)  
  
  
